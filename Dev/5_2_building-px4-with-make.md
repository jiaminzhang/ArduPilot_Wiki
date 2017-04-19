# 利用make在Windows上编译ArduPilot源码，生成支持Pixhawk/PX4的固件

本文介绍如何使用*Make*构建适用于Pixhawk 2，Pixhawk和PX4的ArduPilot。

```
用于构建Pixhawk和Pixhawk2的命令是相同的（使用px4-v2）。 除了Pixracer使用px4-v4之外，其余构建是一样的。
对于旧的（过时）PX4使用make px4-v1。
```

## 构建说明

1. 安装[GitHub for Windows](GitHub for Windows)
2. 确保您的github设置关闭了换行自动转换
  * 当您安装Git时，也会安装“Git Shell（或Bash）”终端。 点击安装后的“Git Shell（或Bash）”图标，并在Git“MINGW32”终端窗口中输入以下内容：
  ```
  git config --global core.autocrlf false
  ```
3. 将ardupilot源码库clone到您的计算机上： 
  * 转到GitHub / ArduPilot / ardupilot网页，然后单击“桌面上的克隆”按钮
  * 警告：请注意目录路径小于50个字符。 例如“C：\ Users \ rmackay9 \ Documents \ GitHub \ ardupilot”足够短，但“C：\ Users \ rmackay9 \ Documents \ GitHub \ rmackay9-ardupilot”太长。 这个限制是因为在编译过程中创建的临时文件的路径长度可以超过Windows的260字符路径限制。

初始化和更新子模块
```
git submodule update --init --recursive
```

下载并安装*PX4 toolchain*[pixhawk_toolchain_installer_latest.exe](http://firmware.ardupilot.org/Tools/PX4-tools/pixhawk_toolchain_installer_latest.exe)

安装成功后打开*PX4Console*并进入目标目录：

* 启动*PX4Console*。这可以在*开始=>所有程序=>PX4 Toolchain*（Windows 7电脑），或者您可以直接去C：\ px4 \ toolchain \ msys \ 1.0 \ px4_console.bat打开。

* 在PX4Console中导航到特定的ArduPilot目录。 例如，要构建多旋翼，请导航到：
```
cd /c/Users/<username>/Documents/GitHub/ardupilot/ArduCopter
```
通过输入以下命令之一构建固件：

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

编译完成后可以在ArduCopter目录中找到*.px4扩展名的文件。
！[](http://ardupilot.org/dev/_images/PX4_ArduCopter_Build.png)

* 使用Mission Planner地面站：*初始设置*=>*安装固件*，点击安装固件屏幕的*加载自定义固件*。
```
当您编译项目源码时，ArduPilot将添加（PX4Firmware，PX4NuttX，uavcan）作为git子模块。 
如果您在更改子模块之前编译项目源码，您可能会遇到意想不到的错误。 有关故障排除错误信息，请参阅Git子模块。
```

