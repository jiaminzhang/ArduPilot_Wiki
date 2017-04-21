# 库示例草图

探索代码的第一步是使用库的示例草图（example sketches）。 遵循arduino传统，我们为大多数库（libraries）提供了示例草图。 “草图（sketches）”只是一个主cpp程序文件。

了解ArduPilot中使用的库API和约定，对于理解代码至关重要。 所以使用库示例草图是一个很好的入门方式。 作为一个开始，您应该阅读，构建和运行以下库的示例草图：

* libraries/AP_GPS/examples/GPS_AUTO_test
* libraries/AP_InertialSensor/examples/INS_generic
* libraries/AP_Compass/examples/AP_Compass_test
* libraries/AP_Baro/examples/BARO_generic
* libraries/AP_AHRS/examples/AHRS_Test

例如，以下操作将在Pixhawk上构建并安装AP_GPS示例草图：

```
cd $ARDUPILOT_HOME # AruPilot库的顶级目录
./waf configure --board=px4-v2
./waf build --target examples/INS_generic --upload
```

waf可以列出它可以构建的示例：

```
cd $ARDUPILOT_HOME
./waf list | grep 'examples'
```
