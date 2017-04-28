# 线程

## 了解ArduPilot线程

一旦了解了ArduPilot库的基础知识，您就可以了解ArduPilot如何处理线程。 从arduino继承的setup() / loop()结构可能会使ArduPilot看起来像一个单线程系统，但事实上并不是这样。

ArduPilot中的线程方法取决于电路板。 一些电路板（如APM1和APM2）不支持线程，所以做一个简单的定时器和回调。 一些电路板（PX4和Linux）支持丰富的Posix线程模型，具有实时优先级，而且这些模型由ArduPilot广泛使用。

这里有一些与在ArduPilot中需要了解的线程相关的关键概念：

* 定时器回调
* HAL专用线程
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
