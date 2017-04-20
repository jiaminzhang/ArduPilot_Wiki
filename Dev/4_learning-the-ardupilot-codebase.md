# 学习ArduPilot代码架构

ArduPilot代码库相当大（ardupilot核心代码大约70w行），对新用户非常具有挑战性。 本页旨在提供一些有关如何快速入门代码的建议。 本文假设您已经熟悉了C ++的关键概念，目前许多示例假设您将在Linux系统上研究代码。


该页面和下面链接的页面是入门教程。 你应该逐步阅读每个页面。 如果您认为某些重要信息丢失或可以被改进，那么请在[维基提问](https://github.com/ArduPilot/ardupilot_wiki/issues)，我们将尽可能地解决它。

## 教程步骤

* [介绍](Dev/4_1_learning-ardupilot-introduction.md)
* [库介绍](Dev/4_2_apmcopter-programming-libraries.md)
* [库实例图]()
* [传感器驱动]()
* [进程通信]()
* [串口和控制台]()
* [RC输入输出]()
* [存储和EEPROM管理]()
* [EKF]()
* [Copter - 代码介绍]()
* [姿态控制]()
* [添加参数]()
* [添加新的飞行模式]()
* [让你的新代码间歇运行]()
* [避障]()
* [添加一个新的MAVLink协议]()
* [添加一个新的MAVLink平衡环]()

```
目前在ArduPilot中有4种机型（多旋翼，固定翼，小车，穿越机），而不同机型之间有很多共同的元素，也各有各的特点。 现在我们只详细说明了多旋翼的代码架构。
```

## 其他教程

虽然不完全是ArduPilot的一部分，本教程也可能是有用的。

* [DroneKit](http://python.dronekit.io/)

