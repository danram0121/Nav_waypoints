复制参数到指定位置
```
sudo cp transbot_cartographer.launch /opt/ros/melodic/share/cartographer_ros/launch
sudo cp transbot.lua /opt/ros/melodic/share/cartographer_ros/configuration_files 
```

激光雷达
```
roslaunch transbot_nav laser_map.launch map_type:=gmapping
roslaunch transbot_nav laser_map.launch map_type:=hector
roslaunch transbot_nav laser_map.launch map_type:=karto
roslaunch transbot_nav laser_map.launch map_type:=cartographer
```
Astra相机
```
roslaunch transbot_nav camera_map.launch map_type:=gmapping 
roslaunch transbot_nav camera_map.launch map_type:=hector 
roslaunch transbot_nav camera_map.launch map_type:=karto 
roslaunch transbot_nav camera_map.launch map_type:=cartographer 
```

laser————>rviz
```
roslaunch transbot_nav view_laser_map.launch
```
camera————>rviz
```
roslaunch transbot_nav view_camera_map.launch
```
cartographer————>rviz
```
roslaunch transbot_nav view_cartographer.launch
```

ROS 查看图像
```
rqt_image_view  
```
ROS 查看tf树
```
rosrun rqt_tf_tree rqt_tf_tree  
```
ROS 查看节点图
```
rqt_graph
```
dynamic reconfigure
```
rosrun rqt_reconfigure rqt_reconfigure 
```
#### 删除gazebo进程

```
killall gzclient gzserver
```

#### 启动roscore

```
roscore
roscore& --后台启动
```
#### 删除roscore进程

```
killall roscore rosmaster
```
### 

# cartographer

### 1.安装

```
sudo apt-get update
sudo apt-get install ros-melodic-cartographer*
```

### 2.官方案例演示

2Dslam demo演示

```
roslaunch cartographer_ros demo_backpack_2d.launch  bag_filename:=/home/yahboom/Downloads/b0-2014-07-21-12-42-53.bag
或
roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=/home/yahboom/Downloads/cartographer_paper_deutsches_museum.bag
```

启动3Dslam demo演示

```
roslaunch cartographer_ros demo_backpack_3d.launch bag_filename:=/home/yahboom/Downloads/b3-2016-04-05-14-14-00.bag
```

### 3.文件.launch路径：

```
/opt/ros/melodic/share/cartographer_ros/launch
```

### 4.文件.lua路径

```
/opt/ros/melodic/share/cartographer_ros/configuration_files
```

### 5.复制2d数据包（这个包一定要有）

```
/opt/ros/melodic/share/cartographer_ros/configuration_files/
```

### 6.说明

cartographer的建图回环很慢，暂时不明白原因，
建小地图效果还可以，大地图效果可能会不太好（还没测试）

回环判断标准：在rivz界面看到的半透明灰色是未识别（完全陌生环境），
                      灰色是未完全识别（环境不确定），
                      纯白色是完全识别（回环）

因此建图过程尽量缓慢，如果走过一遍没回环，同样的路可以走两遍让他完全回环