##ROS安装实验报告
14353335 谢玉婷
***
###ROS框架描述
ROS(Robot operation system)，是一个用于机器人的次操作系统，或者说是一套框架，底层提供硬件驱动，软件层面支持通用的文件格式。ROS的运行架构是一种使用ROS通信模块实现模块间P2P的松耦合的网络连接的处理架构，它执行若干种类型的通讯，包括基于服务的同步RPC（远程过程调用）通讯、基于Topic的异步数据流通讯，还有参数服务器上的数据存储。但是ROS本身并没有实时性。

###ROS安装与测试笔记
首先按照 http://wiki.ros.org/jade/Installation/Ubuntu 上的步骤完成ROS安装
- 配置sources.list  
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`
- 配置密钥
`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116`
- 安装ROS
  首先更新安装包：
  `sudo apt-get update` 
  选择安装 Desktop-Full Install 版本：
  `sudo apt-get install ros-jade-desktop-full`
  - 初始化rosdep
  `sudo rosdep initrosdep update`
  - 环境配置
  `echo "source /opt/ros/jade/setup.bash" >> ~/.bashrcsource ~/.bashrc`
  -获取rosinstall
  `sudo apt-get install python-rosinstall`

用ROS中的小海龟例子测试ROS安装
- 在新的终端打开roscore
`$ roscore`
以下程序运行在roscore的基础上，一定不能关闭这个终端。
-在新的终端打开运行小海龟界面
`$ rosrun turtlesim turtlesim_node `
- 在新的终端打开鼠标控制终端
`$ rosrun turtlesim turtle_teleop_key `
在鼠标控制终端按方向键盘可控制小海龟移动。
![enter image description here](http://a3.qpic.cn/psb?/V11ttduT1jLeiZ/U.vpZbxPXnO1QWzDfSN9EveRdriZOwOPVCqp8kjcyAI!/b/dAoBAAAAAAAA&bo=SAQNAgAAAAADAGY!&rf=viewer_4)
![enter image description here](http://a2.qpic.cn/psb?/V11ttduT1jLeiZ/DBWTA6G70wF62mLREvHNuFQu5MnMm6xxG.gThuhTa.Y!/b/dAkBAAAAAAAA&bo=YwQgAgAAAAADAGA!&rf=viewer_4)


###实验感想
从小海龟这个例子对ROS框架有了一点基本的认识--ROS框架的设计便利了两个模块之间的通信的实现。在小海龟的例子中，turtlesim_node节点和turtle_teleop_key 节点在ROS 主题上进行通信，turtle_teleop_key在该主题上发送key strokes, turtlesim在相同主题上，预定该key strokes, 从而实现了鼠标控制终端和小海龟绘制终端的通信。



