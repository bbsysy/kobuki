# kobuki (turtlebot2) on melodic (Ubuntu 18.04)



## Prerequisites

* ROS Melodic on  Ubuntu18
* kobuki(turtlebot2)

## How to build Kobuki ROS package

ydlidar package까지 포함된 것

```
Clone this project to your catkin's workspace scr folder
 $ cd catkin_ws
 $ cd src
 $ git clone https://github.com/bbsysy/kobuki.git
 $ cd ..
 $ catkin_make

```



#### lidar가 안될 시

ydlidar_ros 지우고 새로 깔기

```
1. Clone this project to your catkin's workspace src folder
    $ git clone https://github.com/YDLIDAR/ydlidar_ros
2. Running catkin_make to build ydlidar_node and ydlidar_client
    $ catkin_make
3. Create the name "/dev/ydlidar" for YDLIDAR
    $ roscd ydlidar_ros/startup
    $ sudo chmod 777 ./*
    $ sudo sh initenv.sh
```



## How to run Kobuki

```
  roscore
$ roslaunch kobuki_node minimal.launch
$ roslaunch ydlidar_ros lidar.launch
$ roslaunch kobuki_keyop keyop.launch
```

### kobuki_run

#### slam (gmapping)

gmapping.launch files that run kobuki_node, ydlidar, gmapping and rviz all at once

```
$ roslaunch kobuki_run gmapping.launch

At another terminal
$ roslaunch kobuki_keyop keyop.launch
```

##### gmapping2.launch는 rosbag에 저장한 후에 mapping

if you want to use rosbag

```
$ mkdir ~/bagfiles
$ cd ~/bagfiles
$ rosbag record -a

when the recording is over, in a new terminal
$ rosbag info <your bagfile>  (This is for data verification, so it doesn't matter if you don't run it.)
$ rosbag play <your bagfile>
$ roslaunch kobuki_run gmapping.launch
```

first, save the data using rosbag and then gmapping

```
  roscore
$ roslaunch kobuki_node minimal.launch
$ roslaunch ydlidar_ros lidar.launch
$ roslaunch kobuki_keyop keyop.launch

saving data
$ cd ~/bagfiles
$ rosbag record -a
```

You can disconnect from the kobuki.

```
$ rosrun gmapping slam_gmapping _base_frame:="base_footprint"
```

if you want to save the map (with rviz on)

```
$ rosrun map_server map_server -f ~/map_server
```



#### navigation

kobuki_navigation.launch files that run kobuki_node, ydlidar, navigation and rviz all at once

```
$ roslaunch kobuki_run kobuki_navigation.launch
```

