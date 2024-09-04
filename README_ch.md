# 机器人
**Read this in other languages [english](README.md), [中文](README_ch.md).**
该项目旨在为 arduino 大型传感器（SRF08 声纳和 MinIMU-9）和华硕 xtionPro 实时摄像头实现基础节点（侦听器/发布者）。这些节点将在 Ubuntu 18.04 和 ROS 旋律的 Odroid XU4 上运行。 
“SRF08 声纳”和“MinIMU-9”传感器（“LSM6”和“LIS3MDL”）有独立的库。您只需要下载并包含在您的主文件中。

## 图像处理

使用 Asus xtionPRO live 进行 RGB 图像和深度图像。 
如果您在 Windows 上运行，请从 'openni2.initialize（“/usr/lib/”）' ---> 'openni2.initialize（）' 中删除路径。

### 需要的库

要运行代码，您需要使用 'pip install -r requirements.txt' 安装  'requirements.txt' 文件。 
当然，你需要安装一个外部库 'openni2'，你可以在这里找到它（https://structure.io/openni）。 

## Arduino 原理图

![电路]（./circuit.svg）
PS： IC = MinIMU-9。

## ROS


- 首先确保安装“ROS-melodic-desktop”（我在 Ubuntu 18.04 上使用的版本），[你可以在这里找到教程]（http://wiki.ros.org/melodic/Installation/Ubuntu）。
- 安装上一主题中的“python3”库。
  - 尝试运行 './image_processing' 中的一个示例，如果你运行，你就可以
 Go 到 Python 端。
- 安装 [openni2_launch]（http://wiki.ros.org/openni2_launch） 软件包。
- 安装 Arduino IDE 和必要的库，[tutorial]（http://wiki.ros.org/rosserial_arduino/Tutorials/Arduino%20IDE%20Setup）。
  - 如果您想了解更多关于 [Arduino + ROS workpace]（http://wiki.ros.org/rosserial_arduino/Tutorials/CMake）
- 使用 'chmod +x node.py' 使两个 python 节点都可执行，通常它们位于 'workspace/src/SOME_PACKAGE/scripts' 中。
- 有 'tmux， screen' 或类似的东西会很好。

现在要启动工作区，请导航到 './ros_workspace' 并运行 'catkin_make' ，然后运行 'source devel/setup.bash`. 
上传 Arduino 代码 'catkin_make arduino_sensors_firmware_arduino_sensors-upload'。 

启动 ROS 节点：

- 启动 'roscore'。
- 相机主题 'roslaunch openni2_launch openni2.launch'。
- Arduino 节点 'rosrun rosserial_python serial_node.py /dev/ttyACM0'。
- 相机节点 'rosrun camera_rgb_img node.py' 和 'rosrun camera_rgb_img node.py”。
