# 线程

## 了解ArduPilot线程

一旦了解了ArduPilot库的基础知识，您就可以了解ArduPilot如何处理线程。 从arduino继承的setup() / loop()结构可能会使ArduPilot看起来像一个单线程系统，但事实上并不是这样。

ArduPilot中的线程方法取决于电路板。 一些电路板（如APM1和APM2）不支持线程，所以做一个简单的定时器和回调。 一些电路板（PX4和Linux）支持丰富的Posix线程模型，具有实时优先级，而且这些模型由ArduPilot广泛使用。

这里有一些与在ArduPilot中需要了解的线程相关的关键概念：

* 定时器回调
* HAL特殊线程
* 驱动程序专用线程
* ardupilot驱动程序与平台驱动程序
* 平台特定的线程和任务
* AP_Scheduler系统
* 信号量
* 无锁数据结构

#### 定时器回调

每个平台在AP_HAL中提供1kHz定时器。 ArduPilot中的任何代码都可以注册一个定时器功能，然后以1kHz调用。 所有注册的定时器功能都被顺序调用。使用这种非常原始的机制，因为它非常稳定，也非常有用。 通过调用hal.scheduler-> register_timer_process()来注册一个定时器回调，如下所示： 

```
hal.scheduler->register_timer_process(AP_HAL_MEMBERPROC(&AP_Baro_MS5611::_update));
```

该特定示例来自MS5611气压计驱动程序。 AP_HAL_MEMBERPROC()宏提供了一种将C++成员函数封装为回调参数（将对象上下文与函数指针捆绑在一起）的方法。

当一段代码运行至少需要在1kHz的情况下完成，并且如果执行超过1ms，那么它应该保存“上次调用的变量”，立即返回。 可以使用hal.scheduler-> millis()和hal.scheduler-> micros()函数来获取启动后的时间，这两个函数分别以毫秒和微秒为单位。

您现在应该去修改一个现有的示例草图（或创建一个新的示例草图）并添加一个定时器回调。 使定时器自加计数，然后在loop()函数中每秒打印一次计数器的值。 修改您的函数，使其每25毫秒自加一次。

#### HAL特殊线程

在支持实线程的平台上，平台的AP_HAL将创建许多线程来支持基本操作。 例如，在PX4上创建以下HAL特殊线程：

* UART线程，用于读写UART（和USB）
* 定时器线程，支持上述1kHz定时器功能
* IO线程，支持写入microSD卡，EEPROM和FRAM

在每个AP_HAL实现中查看Scheduler.cpp，查看创建的线程以及每个线程的实时优先级。

如果您有Pixhawk，那么您现在还应该设置一个调试控制台，并附加到nsh控制台（串口5）。波特率设置为57600，连接好后，尝试“ps”命令，你会得到这样的东西：
```
PID   PRI   SCHD  TYPE  NP      STATE   NAME
 0    0     FIFO  TASK  READY   Idle    Task()
 1 192 FIFO KTHREAD WAITSIG hpwork()
 2 50 FIFO KTHREAD WAITSIG lpwork()
 3 100 FIFO TASK RUNNING init()
 37 180 FIFO TASK WAITSEM AHRS_Test()
 38 181 FIFO PTHREAD WAITSEM <pthread>(20005400)
 39 60 FIFO PTHREAD READY <pthread>(20005400)
 40 59 FIFO PTHREAD WAITSEM <pthread>(20005400)
 10 240 FIFO TASK WAITSEM px4io()
 13 100 FIFO TASK WAITSEM fmuservo()
 30 240 FIFO TASK WAITSEM uavcan()
```
