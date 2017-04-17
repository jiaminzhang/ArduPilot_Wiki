# 利用ArduPilot项目做开发

本文介绍了获取ArduPilot代码的方式以及如何向项目提交更改。

## 概述

ArduPilot项目使用[git](https://git-scm.com/)进行源代码管理，使用[GitHub](https://github.com/)用于源代码托管。

想要为ArduPilot项目做贡献的开发者可以在GitHub上Fork下来项目源码，在自己Fork下来的项目中创建一个branch分支，添加新功能，然后将更改pull request到“master”项目中。对于只需要使用和编译的开发者，可以从GitHub上clone下来master库，build后使用就可以了。

用于固定翼（Plane），旋翼飞机（Copter），小车（Rover）和穿越机（Antenna Tracker）的ArduPilot项目源代码都可以在https://github.com/ArduPilot/ardupilot 上下载。 PX4平台（即PX4v1和Pixhawk）使用了一些额外的项目：PX4Firmware，PX4NuttX，uavcan - 在构建项目时，这些项目会被导入为Git子模块（通过git submodule update --init --recursive命令）。

MissionPlanner的库在[ardupilot/MissionPlanner](https://github.com/ArduPilot/MissionPlanner)。
