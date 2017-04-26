# 传感器驱动


ArduPilot支持来自不同制造商的各种传感器。 [测距仪](http://ardupilot.org/copter/docs/common-rangefinder-landingpage.html#common-rangefinder-landingpage)（例如：声纳，激光雷达）就是一个标志性的例子。 本页试图解释传感器驱动程序如何编写，以及如何集成到代码中。

## 支持的协议

支持I2C，SPI，UART（串口）和CANBUS（特别是UAVCAN）协议。 如果您打算编写新的驱动程序，则可能需要参考传感器的datasheet，以确定使用哪种协议。

#### I2C

* 一个主机，多个从机
* 一种相对简单的协议，适用于短距离通信（即小于1m）。
* 总线运行在100kHz或400kHz，但与其他协议相比，数据速率相对较低。
* 只需要4个引脚（VCC，GND，SDA，SCL）

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver-i2c1.png)

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver-i2c2.png)

#### SPI

* 一个主机，一个从机
* 速度20Mhz +，意味着与I2C相比非常快
* 只能在短距离（10cm）
* 需要至少5个引脚（VCC，GND，SCLK，MOSI，MISO）+ 1个从机片选引脚

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver-spi1.png)

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver-spi2.png)

#### 串行/ UART
* 一个主机，一个从机
* 协议适用于基于字符的通信，与I2C和SPI（即1m）相比通信距离较长
* 在57Kbps〜1.5Mbps相对较快
* 至少需要4个引脚（VCC，GND，TX，RX）和2个可选引脚（Clear-To-Send, Clear-To-Receive）

#### CAN总线与UAVCAN

* 多主机总线，任何节点可以在需要时发起数据传输
* 基于分组的长距离通信协议
* 高速，通常为1 Mb（但只有在50%速度传输下传输效率较好）
* 至少需要3个引脚（GND，CAN HI，CAN LO）。 可选择VCC为节点供电
* 点到点拓扑。 不建议星状图或树状图
* 在总线的每一端需要终止

![](http://ardupilot.org/dev/_images/code-overview-can-bus.png)

## 前端/后端拆分

传感器驱动程序架构中的一个重要概念是前端/后端拆分。

![](http://ardupilot.org/dev/_images/code-overview-sensor-drivers-febesplit.png)

飞行代码只会进入库（也就是传感器驱动程序）的前端。

在启动时，前端基于传感器自动检测（如，检查已知I2C地址是否响应）或通过使用用户自定义的_TYPE参数（如，RNGFND_TYPE，RNGFND_TYPE2）来创建一个或多个后端。 前端维护指向每个后端的指针，通常位于名为_drivers []的数组中。

用户可设置的参数始终保持在前端。

## 驱动程序的运行方式和什么时候被调用

![](http://ardupilot.org/dev/_images/copter-code-overview-architecture2.png)

上图显示了ardupilot架构的放大视图。 左上角的蓝色框显示了传感器驱动程序的后端是如何在后台线程中运行的。 收集来自传感器的原始数据，转换为标准单位，然后保持在驱动=的缓冲区内。


飞行代码的主线程定期运行（如copter为400hz），并通过驱动前端的方法访问最新的数据。 例如，为了计算最新的姿态估计，AHRS / EKF将从传感器驱动程序的前端读取最新的加速度计，陀螺仪和罗盘数据。

该图像略有泛化，对于使用I2C或SPI的驱动程序，它们必须在后台线程中运行，以防其与传感器的高速通信影响主线程的性能，但是对于驱动程序使用串行（即UART）接口，它可以安全地在主线程中运行，因为底层串行驱动程序本身在后台收集数据并包含一个缓冲区。

## 飞行代码与前端示例

下面的示例显示了飞行代码如何从测距仪（如：声纳，激光雷达）驱动中提取数据。 Copter代码的调度程序以20Hz调用read_rangefinder()方法。 下面是这个方法的图片，最新版本可以在sensors.cpp文件中看到。 rangefinder.update()和rangefinder.distance_cm()方法为调用驱动程序的前端。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver1.png)

以下是测距仪驱动程序的前端更新方法。 这样可以让驱动程序有机会在主线程内进行任何通常处理。 依次调用每个后端的更新方法。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver2.png)

## UART /串行后端示例

接下来是使用串行协议的LightWare后端的更新方法。 如用户维基上所述，串行测距仪可以连接到任何飞行控制器的串行端口，但用户必须通过设置SERIALX_BAUD和SERIALX_PROTOCOL参数指定哪个串行端口以及设置波特率。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver-uart1.png)

在LightWare串行驱动程序的启动代码中，首先通过查找上述参数设置的serial_manager类查找用户想要使用哪个UART。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver8.png)

每当驱动程序的后端update()方法被调用时，它将调用get_reading方法，该方法检查新的字符是否已经从传感器到达，然后进行解码。

如上所述，由于串行协议实现了自己的缓冲，因此传感器中任何数据（参见get_reading方法）的处理都在主线程中运行。 即，没有“register_periodic_callback”，就像您将在I2C和SPI驱动程序中看到的那样。

## I2C后端示例

此示例显示Lightware I2C驱动程序的后端。 在这种情况下，前端获取I2C总线，并在初始化期间将其传递到后端。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver5.png)

后端的init方法然后注册它的“timer”方法使它以20hz的频率被调用。 在定时器方法（图中未标出）中，调用从传感器读取字节的get_reading()方法，并将距离转换为厘米。

## SPI后端示例

本例显示了MPU9250 IMU的后端，包括陀螺仪，加速度计和罗盘。 前端获取SPI总线，并在初始化期间将其传递到后端。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver6.png)

在初始化期间调用start()方法并配置传感器。 它使用信号量来确保在同一总线上不会干扰其他SPI器件。

_read_sample方法被注册，以便在1000hz被调用。 注意，没有必要在_read_sample方法中减少/增加信号量，因为这是作为定期回调代码的一部分完成的。

_block_read方法显示了如何从传感器的寄存器读取数据。

![](http://ardupilot.org/dev/_images/code-overview-sensor-driver7.png)

## 附加建议

当编写传感器驱动程序时，不要包含任何等待或延时代码，因为这将延迟与正在使用的总线相关联的主线程或后台线程。

如果写了一个新的库，它必须被添加到飞行目录（即ardupilot / ArduCopter / make.inc和/ ardupilot / ArduCopter / wscript）中的make.inc和wscript文件中，以便链接时能够找到。



