# Copter介绍

Copter是一个先进的开源自动驾驶仪系统，适用于多旋翼和直升机。

## 概述

Copter为多电机控制提供一种完全开源的自动驾驶仪解决方案，不仅可以通过遥控器（RC, Romote Control）实现多种飞行模式控制，而且可以实现任务规划，自主飞行。

作为更广泛的ArduPilot软件平台的一部分，它与地面站（GCS, Ground Control Station）无缝工作，可以通过数传监控飞机和执行任务规划。 它还受益于Ardupilot生态系统的其他部分，包括模拟器，日志分析工具和用于飞机管理和控制的更高级API。

Copter处于空中机器人的前沿，为想要尝试先进技术，前沿技术和开启崭新飞行方式的人们而生。 它已经是许多商用飞控的首选平台，仅仅是因为它十分容易二次开发！

![copter-introduction-diagram](http://ardupilot.org/copter/_images/copter-introduction-diagram.jpg)

## 主要功能

主要功能如下：

* 超牛的自稳和姿态控制：飞行稳如狗；具有“简单（simple）”或“超简单（super simple，即无头模式）”的飞行模式，这一切造就了世界最容易飞的飞机。
  不用担心飞机机头在哪 - 你往前推杆就往前飞，因为飞控懂你！
* 具有自动起飞和自动降落功能（Automatic takeoff and landing）：拨一下开关，飞机就可以全自主地规划路径，自动回家、自动着陆。
* 悬停模式（Loiter）：飞机将使用其GPS和高度传感器来保持其三维空间中某一点的位置。
* 一键返航（RTL, Return to launch）：拨动一个开关就可以让飞机自动回到起飞点。
* 失控保护（Fail safety）：如果检测飞机丢失遥控信号（或位于定义的地理围栏之外），则返回起飞点。如果检测到硬件故障，也会尝试安全着陆。
* 无需编程：使用桌面版Mission Planner软件就可以烧录Ardupilot固件（只需点击一下）并设置飞机。Mission Planner（和其他兼容地面站）具有显示飞机状态，设置飞机参数，通过地图规划飞行路径等强大功能。
* 任务规划可以达到数百个GPS航点（Waypoints）:只需在Mission Planner地面站点击设置航点，飞机就能够自主飞行。你甚至可以设置成自动执行整个任务，包括摄像头控制！唯一需要考虑的是你飞机电池续航是否足够。
* 在飞行中任务规划：使用数传连接后，可以在飞行中更航点和模式，甚至可以用地面站在飞机飞行过程中动态调参！

## 入门

如果您正在使用使用Copter固件的到手即飞的飞机，那么可能已经设置，配置和调整好了飞机。我们建议您在飞行前阅读制造商的说明，特别是与安全相关的说明。

一旦您熟悉飞控的默认设置，您可能需要配置您的遥控器和飞控来实现更具挑战性的飞行模式，或选择地面站开始任务规划飞行。

```
注意:无论是到手即飞的飞机，还是自己DIY的飞机，自驾都有潜在的危险！ 始终遵循最佳安全措施，并密切注意所有安全警告。
```


如果您正在DIY一架飞机，该维基拥有您需要的一切！ 您应该首先阅读本节以了解多旋翼可以做什么，以及如何选择一个机架，飞行控制器以及其他基本组件。然后，您可以进入首次设置，了解如何组装您的飞机，然后首次飞行，以了解如何配置和调整。

## 开发团队

Copter固件由来自开源社区的志愿者专门开发和维护。你可以在它们开发的基础上二次开发或者在ArduPilot’s Discuss Server查看新项目。

*我们所有参与这个项目的人都非常关心与我们分享这个星球的人的隐私和安全。请善待这项技术。它是众多开发者花费掉许多晚上和周末的产物，我们开源它，是希望与大家分享，使它更酷。*

## 了解更多关于Copter

要了解更多关于Copter和主要配置的设置，请参阅以下主题：

* 多旋翼工作原理
* 你需要什么组件
* 安全问题
* 选择机架
* 选择飞行控制器
* 选择地面站
* 用例概述
