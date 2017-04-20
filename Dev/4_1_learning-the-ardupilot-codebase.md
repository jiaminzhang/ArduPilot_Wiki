# 介绍

本页介绍了ArduPilot代码的基本结构。在开始之前，您应该想明白你要用代码中的哪一部分。您只需使用浏览器登录https://github.com/ArduPilot/ardupilot/ ，就能看到源码文件目录，可以选择下载某一部分，但如果用git克隆的话，你会下载所有源码库。
你可以使用一款好用的开发者IDE打开下载的源码，[推荐软件](Dev/code-editing-tools-and-ides.md)。

## 基础架构

![](http://ardupilot.org/dev/_images/ArduPilot_HighLevelArchecture.png)

ArduPilot的基本结构分为5个主要部分：

* 机型代码(ArduCopter、ArduPlane登)
* 共享库（shared libraries）
* 硬件抽象层（AP_HAL）
* 工具目录（Tools）
* 外部支持代码（如mavlink，dronekit）

## 不同机型代码

下载的源码目录下包含多种机型的代码，主要分为4大类：Plane, Copter, APMrover2 和 AntennaTracker.。虽然不同机型之间有很多共同的要素，但它们也各有不同。 现在我们只详细说明Copter的代码。

除了* .cpp文件，每个机型目录下都包含一个列出库依赖关系的make.inc文件。 Makefile读取此内容以创建-I和-L标志来构建程序。

## 共享库

这些共享库（[libraries](https://github.com/ArduPilot/ardupilot/tree/master/libraries)）共同为Copter, Plane, Rover and AntennaTracker服务。这些库包括传感器驱动，姿态和位置估计（也称为EKF）和控制代码（即PID控制器）。
有关更多详细信息，请参阅[库说明](Dev/apmcopter-programming-libraries.md)，[库示例草图](Dev/learning-ardupilot-the-example-sketches.md)和[传感器驱动](Dev/code-overview-sensor-drivers.md)程序页面。

## 硬件抽象层（AP_HAL） 

AP_HAL层（硬件抽象层）是为了使ArduPilot兼容不同平台。libraries/AP_HAL路径下定义了不同硬件的代码接口，然后每个类型电路板都有一个AP_HAL_XXX子目录，例如基于AVR的电路板的AP_HAL_AVR，Pixhawk电路板的AP_HAL_PX4和基于Linux的电路板AP_HAL_Linux。

## 工具目录

工具目录是各种支持目录。 例如，tools / autotest提供autotest.ardupilot.org网站后面的自动测试基础设施，并且tools/ Replay提供了我们的日志重放工具。

## 外部支持代码

在某些平台上，我们需要外部支持代码来提供额外的功能或板级支持。目前的扩展部分是：

[PX4NuttX](https://github.com/ArduPilot/PX4NuttX) - Pixhawk板上使用的核心NuttX RTOS。

[PX4Firmware](https://github.com/ArduPilot/PX4Firmware) - Pixhawk主板上使用的基本PX4中间件和驱动程序。

[uavcan](https://github.com/ArduPilot/uavcan) - 在ArduPilot中使用的uavcan CANBUS实现。

[mavlink](https://github.com/mavlink/mavlink) - mavlink协议和代码生成器。

```
当您构建ArduPilot时，它们中的大多数都作为Git子模块导入。
```
