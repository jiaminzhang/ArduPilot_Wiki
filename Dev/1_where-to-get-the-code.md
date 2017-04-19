# 利用ArduPilot项目做开发

本文介绍了获取ArduPilot代码的方式以及如何向项目提交更改。

## 概述

ArduPilot项目使用[Git](https://git-scm.com/)进行源代码管理，使用[GitHub](https://github.com/)用于源代码托管。

想要为ArduPilot项目做贡献的开发者可以在GitHub上Fork下来项目源码，在自己Fork下来的项目中创建一个branch分支，添加新功能，然后将更改pull request到“master”项目中。对于只需要使用和编译的开发者，可以从GitHub上clone下来master库，build后使用就可以了。

用于固定翼（Plane），旋翼飞机（Copter），小车（Rover）和穿越机（Antenna Tracker）的ArduPilot项目源代码都可以在https://github.com/ArduPilot/ardupilot 上下载。 PX4平台（即PX4v1和Pixhawk）使用了一些额外的项目：
[PX4Firmware](https://github.com/ArduPilot/PX4Firmware)，[PX4NuttX](https://github.com/ArduPilot/PX4NuttX)，[uavcan](https://github.com/ArduPilot/uavcan) - 在构建项目时，这些项目会被导入为[Git子模块]()。

MissionPlanner的库在[ardupilot/MissionPlanner](https://github.com/ArduPilot/MissionPlanner)。

```
由于历史遗留问题，老版本的Google Code库还在网上存在，\
除非您特别需要较旧的（APM 1.x）资源，否则不要使用它。
```

## 必备条件

ArduPilot项目使用git进行源代码管理。

Git可在所有主流操作系统上使用，并且存在各种工具使得更易入门。 首先，您需要下载并[安装客户端](https://git-scm.com/downloads)。 如果您刚开始使用源代码控制系统，您可以使用桌面版的[GitHub for Windows/GitHub for Mac](https://desktop.github.com/)客户端软件作为入门，它与GitHub完美集成。 本指南会介绍通过GitHub for Windows用户界面以及通过OSX / Linux终端的命令行界面来使用GitHub。

如果您期望将代码提交到官方APM源代码库，则需要使用Github注册一个免费的用户帐户。

## 学习使用Git

本指南介绍了使用项目所需的基本git命令/概念：clone，branch，commit，push。

如果您想了解更多有关git的信息，那么在线有很多很棒的资源。 这里只是几个你可能会发现有用的：

[Try Git](https://try.github.io/levels/1/challenges/1)：基于浏览器的互动教程，用于学习git。\
[Git Ready](http://gitready.com/)：各种难度级别的教程。\
[Git SCM Book](http://git-scm.com/book/en/Getting-Started)：介绍和完整文档。

## Fork源码主库

```
如果您只想编译和测试项目源代码（不进行更改），则可以跳过此步骤，然后clone主项目库（下一节）。
```
“Fork”是GitHub将源码库复制到您自己的GitHub帐户的术语(在网上从别人的账户复制到自己网上的账户)。Fork后的源码库保留有关原始项目的信息，以便您可以从中获取更新（并向其提供更改）。如果要将更改提交给主项目，则需要首先创建自己的主ArduPilot库的分支。

Fork主源码库：

* 登录Github并转到https://github.com/ArduPilot/ardupilot。
* 右上方Fork按钮：

![](http://ardupilot.org/dev/_images/APM-Git-Github-Fork-300x641.jpg)

点击Fork按钮并按照说明进行操作。

完成后，您的帐户中将会有一个新的源码库：//github.com/your-github-account-name/ardupilot

Fork下来这个源码库，你就可以clone后在本地进行代码更改了。

## Clone源码库

“Clone”是git的术语，用于在您自己的计算机上制作任何源码库的副本（相当于把网上的源码库复制到你自己的电脑硬盘上）。 您可以Clone自己先前Fork下来的源码库（如果要更改源代码）或直接Clone主ArduPilot源码库。

Clone项目所需的信息/工具位于每个库的Github主页的屏幕右侧。

![](/Dev/clone.png)

*GitHub上Clone库的界面*

#### OSX/Linux Terminal:
* 打开终端并进入要clone项目的目录
* Clone你Fork下来的项目：
```
git clone https://github.com/your-github-account-name/ardupilot
cd ardupilot
git submodule update --init --recursive
```
或者直接在主项目clone:
```
git clone https://github.com/ArduPilot/ardupilot
cd ardupilot
git submodule update --init --recursive
```

#### Windows (GitHub GUI): 
* 在浏览器中打开[ardupilot/ardupilot](https://github.com/ArduPilot/ardupilot)存储库
* 点击下图中的的“Open in Desktop”按钮
![](/dev/Open-in-desktop.png)
* 如果你以前没有安装GitHub：
  * 当被带到windows.github.com页面时，按下右上角的“download”按钮 
  ![](http://ardupilot.org/dev/_images/CloningTheRepository_Windows_DownloadGithub.png)
  * 将**GitHubSetup.exe**下载到电脑上，然后按照说明安装GitHub客户端 
  * 在GitHub客户端上，单击右箭头按钮可查看最近提交的列表或鼠标右键单击ardupilot / ardupilot库并点击“open in explorer”，在资源管理器中打开。 
  ![](http://ardupilot.org/dev/_images/CloningTheRepository_Windows_OpenGithub.png)
  * 您现在也可以在自己喜欢的编辑器中打开文件，例如[NotePad ++](https://notepad-plus-plus.org/)，[Sublime Text](http://www.sublimetext.com/)或[Acme](http://acme.cat-v.org/)。 
  
## 编译代码
