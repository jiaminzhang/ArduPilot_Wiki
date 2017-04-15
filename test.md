# Copter介绍

Copter是一个先进的开源自动驾驶仪系统，适用于多旋翼，直升机和小车等。

## 概述

Copter为多电机控制提供一种完全开源的自动驾驶仪解决方案，不仅可以通过遥控器（RC, Romote Control）实现多种飞行模式控制，而且可以实现任务规划，自主飞行。

作为更广泛的ArduPilot软件平台的一部分，它与地面站（GCS, Ground Control Station）无缝工作，可以通过数传监控飞机和执行任务规划。 它还受益于Ardupilot生态系统的其他部分，包括模拟器，日志分析工具和用于飞机管理和控制的更高级API。

Copter处于空中机器人的前沿，为想要尝试先进技术，前沿技术和开启崭新飞行方式的人们而生。 它已经是许多商用飞控的首选平台，仅仅是因为它十分容易二次开发！

![copter-introduction-diagram](http://ardupilot.org/copter/_images/copter-introduction-diagram.jpg)

## 主要功能

主要功能如下：

* 超牛的自稳和姿态控制：飞行稳如狗；具有“简单（simple）”或“超简单（super simple，即无头模式）”的飞行模式，这一切造就了世界最容易飞的飞机。
* 不用担心飞机机头在哪 - 你往前推杆就往前飞，因为飞控懂你！
* 具有自动起飞和自动降落功能（Automatic takeoff and landing）：拨一下开关，飞机就可以全自主地规划路径，自动回家、自动着陆。
* 悬停模式（Loiter）：飞机将使用其GPS和高度传感器来保持其三维空间中某一点的位置。
* 一键返航（RTL, Return to launch）：拨动一个开关就可以让飞机自动回到起飞点。
* 失控保护（Fail safety）：如果检测飞机丢失遥控信号（或位于定义的地理围栏之外），则返回起飞点。 如果检测到硬件故障，也会尝试安全着陆。



