# 开始PX4的开发
官方教程：https://docs.px4.io/main/zh/development/development.html
源代码：https://github.com/PX4/PX4-Autopilot
参考：https://gitcode.csdn.net/662f74c8ef0d142cbb2c8249.html

## 从代码结构入手
进入源代码目录，可以看到以下主要目录
### boards
borads 文件夹是各个品牌版本的飞控的编译脚本，其中px4文件夹壮的是pixhawk的原生固件的编译脚本和配置
这些编译脚本和配置决定了哪些驱动文件、功能模块会被编译进固件。如果见出现固件大小过大无法烧录的问题，则可以在这里进行固件裁剪

### build
build文件夹是编译目标目录，只有至少编译过一次才会生成

### camke
cmake文件夹是cmake编译工具的相关文件。正常情况下不用修改

### launch
仿真环境使用

### msg
msg文件夹内是uORB消息主题。实现PX4各进程之间通信就是用这些message。这里可以在这个文件夹内定义自己的message

### ROMFS
ROM FILE SYSTEM，只读文件系统。这里存放了启动时运行的脚本，负责系统初始化
在px4fmu_common文件夹中的init.d是px4系统初始化上电启动的启动脚本，比较重要的是
rcS：最先启动的脚本，负责挂载sd卡，启动uORB，配置系统参数
rc.logging: 日志系统
rc.sensors: sensors驱动启动代码
rc.mc_apps: 启动上层应用Attitude/Position estimator, Attitude/Position control.

### platforms
操作系统的实现，NuttX

### src
源代码目录，PX4的核心业务代码
drivers：传感器驱动代码，包括陀螺仪、加速度计、磁力计、气压计、GPS、等
examples：官方给出的简单例程，方便开发者入门开发
lib：标准库，有矩阵计算、pid控制、传感器校准等算法
modules：功能模块文件夹，这里是姿态解算、姿态控制、位置估计、位置控制、落地检测、传感器初始化等模块。
