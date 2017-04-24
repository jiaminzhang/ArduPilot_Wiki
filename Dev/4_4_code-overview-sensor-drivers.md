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
