# 利用Eclipse在Windows上生成Pixhawk/PX4版本的固件

本文介绍如何设置Eclipse来编辑ArduPilot代码并编译生成Pixhawk/PX4固件。

```
在Eclipse运行之前，请确保安装了Java（32位），否则由于32位/ 64位版本不匹配，
您将得到Java错误代码13。[点击安装Java](https://www.java.com/en/)。
```

## 准备工作

按照“构建Pixhawk / PX4 Windows”中的说明进行下载所需的源代码（*ardupilot，PX4Firmware和PX4NuttX*）和工具链（PX4 toolchain）。

*PX4工具链*包括Eclipse，已经配置成适用ArduPilot源码开发。


## 启动Eclipse

使用PX4工具链安装的PX4 Eclipse链接启动Eclipse。 该链接可以从以下任一访问：

* 点击左下角开始图标 (开始 | 所有程序 | PX4 Toolchain | PX4 Eclipse)
* 或者直接去文件路径下运行： C:\Pixhawk_Toolchain\toolchain\msys\1.0\px4_eclipse.bat

您可以设置一个Eclipse项目“从头开始”，或使用源码中项目文件构建ArduPilot。使用项目文件可以节省您一些工作，因为它们设置好了项目架构，并且设置成px4-v2编译生成“Copter 和“Plane”的固件。

## 用模板文件创建项目

该项目可以从预定义的模板文件创建：

* 将/ardupilot/eclipse.cproject重命名为.cproject，将/ardupilot/eclipse.project重命名为.project
```
注意
如果在Windows下直接把eclipse去掉保存，会要求必须键入文件名。
这时可以在文件最后面添加“.”- 例如**.cproject.**，这时再保存就可以了。
```

* 依次点击 File | Import | General | Existing Projects into Workspace
* 选中 Select root directory，然后点击browse，选择ardupilot源码的路径
* 选中ardupilot路径，然后点击 Finish

![](http://ardupilot.org/dev/_images/EditingWithEclipse_ImportProject.png)

## 从头开始创建项目

替代上述步骤，可以通过执行以下操作创建项目：

* 选择 File | New | Make Project with Existing Code
* 填写项目名称Project Name，设置Existing Code Location为ArduCopter路径
* 将工具链设置为Cross GCC，然后点击Finis

![](http://ardupilot.org/dev/_images/EditingTheCode_Eclipse2.png)

## 使用空格而不是tabs

默认情况下，Copter，Plane 和Rover 将使用空格代替制表符。 这可以通过更改两个设置在Eclipse中设置：

* 选择 Window | Preferences | General | Editors | Text Editors | Insert spaces for tabs.
！[](http://ardupilot.org/dev/_images/EditingTheCode_Eclipse_spaces1.png)
* 选择 Windows | Preferences | C/C++ | Code Style | Formatter，点击New创建一个新的 (例如 “K&R Tab”)，“Indentation” 中设置为“Spaces only”
![](http://ardupilot.org/dev/_images/EditingTheCode_Eclipse_spaces2.png)

## 指定编译路径

在Project Explorer中，右键单击ardupilot文件夹，然后选择“Properties”。 然后在C / C ++ Build下，将“Build location”设置为“Copter ”或“Plane ”的路径，如下所示。

![](http://ardupilot.org/dev/_images/EditingTheCode_Eclipse6.png)

## 指定make目标

在右侧的“Make target”窗口中，创建任何这些目标（可以在px4_targets.mk中找到可能的目标的完整列表）：

命令   |  说明
---|---
make px4-v2   | 为四旋翼（Quad）编译Pixhawk / Pixhawk2可以固件（二者相同）
make px4-v4   | 为四旋翼（Quad）编译PixRacer固件
make px4-v2-hexa  | 编译一个六旋翼的Pixhawk固件。＃其他支持的后缀包括“octa”（六旋翼），“octa-quad”，“tri”（三旋翼），“single”（单旋翼）和“heli”（直升机）。＃更多可以在“mk / targets.mk”中找到
make px4   | 构建用于四角直升机的PX4（过时）和PixHawk固件
make clean  | “清理”ardupilot目录
make px4-clean  | “清洁”PX4Firmware和PX4NuttX目录，以便下次的构建将完全重建它们
make px4-cleandep   |	来自PX4Firmware和PX4NuttX目录的“clean”.d和.o文件。 与“px4-clean”相比，更快但不太完整的重建
make px4-v2-upload  | 构建并烧录Pixhawk的四旋翼固件（即无需使用地面站上传）

例如，下图显示了如何定义px4-v2 make目标。
![](http://ardupilot.org/dev/_images/EditingTheCode_Eclipse3.png)

```
目前还没有上传除quad以外机架的选项。
```
## 构建

制作目标可以通过推绿色圆圈+锤子图标来构建。 构建进度将显示在“Console ”窗口中。
![](http://ardupilot.org/dev/_images/EditingTheCode_Eclipse4.png)
生成的固件保存在相应目录（例如ArduCopter），后缀名为.px4。



