# 库示例草图

探索代码的第一步是使用库的示例草图（example sketches）。 遵循arduino传统，我们为大多数库（libraries）提供了示例草图。 “草图（sketches）”只是一个主cpp程序文件。

了解ArduPilot中使用的库API和约定，对于理解代码至关重要。 所以使用库示例草图是一个很好的入门方式。 作为一个开始，您应该阅读，构建和运行以下库的示例草图：

* libraries/AP_GPS/examples/GPS_AUTO_test
* libraries/AP_InertialSensor/examples/INS_generic
* libraries/AP_Compass/examples/AP_Compass_test
* libraries/AP_Baro/examples/BARO_generic
* libraries/AP_AHRS/examples/AHRS_Test

例如，以下操作将在Pixhawk上构建并安装AP_GPS示例草图：（上述命令在windows平台下的PX4 Console下不能执行，需要在Linux平台下（或者在Windows10下的Ubuntu下））

```
cd $ARDUPILOT_HOME # AruPilot库的顶级目录，也就是/ardupilot目录
./waf configure --board=px4-v2
```
执行结果如下图：

![](/Dev/waf-px4-v2.png)

构建examples/INS_generic，并烧录到飞控中：
```
./waf build --target examples/INS_generic --upload
```
提示重新插拔USB：

![](/Dev/waf-upload.png)

执行成功结果如下图：

![](/Dev/waf-build.png)

waf可以列出它可以构建的示例：

```
cd $ARDUPILOT_HOME
./waf list | grep 'examples'
```

烧录完示例后，您可以通过连接到控制台来查看输出。 控制台取决于电路板的类型。 
在PX4板（即PX4v1和Pixhawk）上，它用USB连接。 所以只需用你最喜欢的串口程序连接USB设备（波特率并不重要）。

例如，如果您安装了mavproxy，可以在Linux上连接Pixhawk：

```
mavproxy.py --setup --master /dev/serial/by-id/usb-3D_Robotics_PX4_FMU_v2.x_0-if00
```

使用-setup选项将mavproxy置于原始串行模式，而不是处理MAVLink模式。 这就是您所需要的示例草图。

## 了解示例草图代码

当您正在阅读示例草图代码（如[GPS_AUTO_test](https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP_GPS/examples/GPS_AUTO_test/GPS_AUTO_test.cpp)代码）时，您会注意到一些似乎很奇怪的事情：

* 它声明一个“hal”引用变量
* 代码很粗略，注释很随意
* setup()和loop()函数

#### hal引用

每个使用AP_HAL功能的文件需要声明一个hal引用。这允许访问AP_HAL :: HAL对象，该对象提供对所有硬件特定功能的访问，包括向控制台打印消息，延时，与I2C和SPI总线通信等。

实际的hal变量隐藏在特定的AP_HAL_XXX库中。 在每个文件中的引用只是提供了一个方便的方法来获得hal。

最常用的hal功能有：

* hal.console-> printf（）来打印字符串
* AP_HAL :: millis（）和AP_HAL :: micros（）从引导开始获取时间
* hal.scheduler-> delay（）和hal.scheduler-> delay_microseconds（）实现短时间延时
* halgpio-> pinMode（），hal.gpio-> read（）和hal.gpio-> write（）用于访问GPIO引脚
* I2C通过hal.i2c访问
* SPI通过hal.spi访问

您可以去libraries/AP_HAL路径下，查看HAL可用功能的完整列表。

#### setup（）和loop（）函数

您将注意到，每个草图都有一个setup（）函数和loop（）函数。 板子启动时调用setup（）函数。 实际的调用来自每个电路板的HAL，所以main（）函数隐藏在HAL中，然后在板子特定启动完成后调用setup（）。

setup（）函数只调用一次，用来初始化库，您可以打印一个“hello”来显示它运行正常。

在setup（）完成之后，loop（）函数被连续调用（通过AP_HAL中的主代码）。 草图的主要工作通常在loop（）函数中。

请注意，这个setup（）/ loop（）安排只是更复杂的电路板的冰山一角。 这可能使得ArduPilot看起来像是单线程的，但事实上还有更多的事情发生，而在具有线程（如PX4和Linux的主板）的板上，实际上将会有很多实时线程启动。 请参阅下面了解ArduPilot线程的部分。

## AP_HAL_MAIN（）宏

你会注意到每个草图底部都有一条这样的一行代码：

AP_HAL_MAIN（）;
这是一个HAL宏，它生成必要的代码来声明一个C ++主函数，以及HAL的任何板级初始化代码。 你无需关心它是如何工作的，但如果你想继续深究，你可以在每个HAL的AP_HAL_XXX目录中查找#define。 它通常在AP_HAL_XXX_Main.h中。

## 粗略示例代码

您将注意到，示例草图非常粗糙，并被严重评论。 这是您为代码做出贡献的机会！ 当您阅读示例草图并探索其工作原理时，会向代码中添加一些注释来解释API，然后提交拉取请求，以便其他人可以从您的学习中受益。
