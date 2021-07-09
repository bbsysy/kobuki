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

