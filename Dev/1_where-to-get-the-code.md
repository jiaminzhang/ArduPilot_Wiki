# 利用ArduPilot项目做开发

本文介绍了获取ArduPilot代码的方式以及如何向项目提交更改。

## 概述

ArduPilot项目使用[Git](https://git-scm.com/)进行源代码管理，使用[GitHub](https://github.com/)用于源代码托管。

想要为ArduPilot项目做贡献的开发者可以在GitHub上Fork下来项目源码，在自己Fork下来的项目中创建一个branch分支，添加新功能，然后将更改pull request到“master”项目中。对于只需要使用和编译的开发者，可以从GitHub上clone下来master库，build后使用就可以了。

用于固定翼（Plane），旋翼飞机（Copter），小车（Rover）和穿越机（Antenna Tracker）的ArduPilot项目源代码都可以在https://github.com/ArduPilot/ardupilot 上下载。 PX4平台（即PX4v1和Pixhawk）使用了一些额外的项目：[PX4Firmware](https://github.com/ArduPilot/PX4Firmware)，[PX4NuttX](https://github.com/ArduPilot/PX4NuttX)，[uavcan](https://github.com/ArduPilot/uavcan) - 在构建项目时，这些项目会被导入为Git子模块（通过git submodule update --init --recursive命令）。

MissionPlanner的库在[ardupilot/MissionPlanner](https://github.com/ArduPilot/MissionPlanner)。

```
由于历史遗留问题，老版本的Google Code库还在网上存在，除非您特别需要较旧的（APM 1.x）资源，否则不要使用它。
```

# 必备条件

ArduPilot项目使用git进行源代码管理。

Git可在所有主流操作系统上使用，并且存在各种工具使得更易入门。 首先，您需要下载并[安装客户端](https://git-scm.com/downloads)。 如果您刚开始使用源代码控制系统，您可以使用桌面版的[GitHub for Windows/GitHub for Mac](https://desktop.github.com/)客户端软件作为入门，它与GitHub完美集成。 本指南会介绍通过GitHub for Windows用户界面以及通过OSX / Linux终端的命令行界面来使用GitHub。

如果您期望将代码提交到官方APM源代码库，则需要使用Github注册一个免费的用户帐户。

# 学习使用Git

本指南介绍了使用项目所需的基本git命令/概念：clone，branch，commit，push。

如果您想了解更多有关git的信息，那么在线有很多很棒的资源。 这里只是几个你可能会发现有用的：

[Try Git](https://try.github.io/levels/1/challenges/1)：基于浏览器的互动教程，用于学习git。
[Git Ready](http://gitready.com/)：各种难度级别的教程。
[Git SCM Book](http://git-scm.com/book/en/Getting-Started)：介绍和完整文档。
