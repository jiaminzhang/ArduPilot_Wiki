# ArduPilot共享库

旋翼飞机（Copter）、固定翼（Plane）和小车（Rover）共享libraries文件。下面是库的顶级目录和他们功能的介绍。
blending
### 内核库:

* [AP_AHRS](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_AHRS) - 使用DCM或者EKF姿态解算
* [AP_Common](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_InertialNav) - 所有模块所需的公共库
* [AP_Math](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Math) - 数学函数库，包括相对有用的向量运算
* [AC_PID](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AC_PID) - PID控制器的库
* [AP_InertialNav](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_InertialNav) - 惯性导航库，与加速度计、GPS和气压计数据融合
* [AC_AttitudeControl](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AC_AttitudeControl) - ArduCopter的控制库，包括姿态控制、位置控制和PID控制
* [AP_WPNav](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_InertialNav) - 航点导航库
* [AP_Motors](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Motors) - 多旋翼和传统直升机电机混合
* [RC_Channel](https://github.com/ArduPilot/ardupilot/tree/master/libraries/RC_Channel) - 将pwm输入/输出从APM_RC转换为内部单位，如角度
* [AP_HAL, AP_HAL_AVR, AP_HAL_PX4](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_HAL_AVR) - 实现了“硬件抽象层”的库，它提供了一值的接口与更高层通信，使其可以更容易地移植到不同的硬件上。
    
### 传感器驱动库:

* [AP_InertialSensor](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_InertialSensor) - 读取陀螺仪和加速度计数据，执行校准并以标准单位提供数据（deg / s，m / s）到主要代码和其他库
* [AP_RangeFinder](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_RangeFinder) - 声呐和ir距离传感器接口库
* [AP_Baro](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Baro) - 气压计接口库
* [AP_GPS](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_GPS) - gps接口库
* [AP_Compass](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Compass) - 轴磁力计接口库
* [AP_OpticalFlow](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_OpticalFlow) - 光流传感器接口库

### 其他库:

* [AP_Mount, AP_Camera, AP_Relay](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Camera) - 相机云台控制库、相机快门控制库
* [AP_Mission](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Mission) - 从eeprom存储/检索任务命令
* [AP_Buffer](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_Buffer) - 一个用于惯性导航的简单FIFO缓冲区
