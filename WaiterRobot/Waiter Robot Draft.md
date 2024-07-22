## step 2 (quality of life)
better ui for movement, seems this is not extrictly necesary , but will help with making testing faster.

- ros2 options to send linear and angular speed. 
	- this two packages seem to do something like it?
	- http://wiki.ros.org/diffdrive_arduino
	- http://wiki.ros.org/differential_drive
	-  **mouse_teleop**: For teleoperation using a mouse. <mark> to fucking anying using something else</mark>
 
	- **joy_teleop**: A generic joystick interface for topics and actions.
	- **key_teleop**: A lightweight console keyboard teleoperation tool.
- own python program
- web somehow
- a hardware option!
---
### step 3
return location using dead reckoning. 

using cmd_vel messages guess the position. 

**option a :** defaoult values for the robot , create a robot modle to see it in rviz or something else
**option b :** values that can change to calibrate the robot considering motors might be diferent

tf2 for robot and for world, frame of reference. 

how to simulate this. 
the basic concept is to input cmd_vel twist messages and have as output the location of the robot

seems there are diferent ways to acomplish this. 

option 1. 
user inputs thru teleop keyboard. a python node reads this , the python bit has a world tf2 and then a robot base that is modified by the twist messages. in this basic example the robot is a diferential robot and the vairables like wheel radios wheel distance are global variables in the python file 


---
### step 4 
go to goal 

---
### step 5 
go to goal avoid obstacles

---
## Research

this helps you find all the exectuables 

```
ros2 pkg executables | grep 'teleop'
``` 

ros2 pkg list | grep mouse_teleop

nav2, or Navigation2, is the second generation of the ROS Navigation stack, designed specifically for ROS 2. It provides tools and libraries to enable autonomous navigation for robots, allowing them to safely move from one location to another in complex environments. Here's an overview of Navigation2:

base_local_planner

robot_localization

**RTABmap**

**AMCL (Adaptive Monte Carlo Localization)**:

**"localization packages"** or **"state estimation packages"**

**ORB_SLAM 2 porting to ROS2**:

**ORB-SLAM3 on turtlebot3 in ROS2 Humble**:

**UZ-SLAMLab/ORB_SLAM3 on GitHub**:

**Cartographer**:

- Cartographer is another SLAM system that provides real-time simultaneous localization and mapping in both 2D and 3D.

**VINS-Mono**:

- VINS-Mono is a SLAM algorithm that uses an IMU. While the exact compatibility with ROS 2 Humble is not mentioned, it's noted as one of the SLAM algorithms that utilize an IMU.
    - [Source: Labbook UvA Rescue 2022](https://staff.fnwi.uva.nl/a.visser/research/roboresc/Labbook)

**SLAM Toolbox**:

- This appears in the related searches, suggesting that SLAM Toolbox might be another SLAM package of interest. However, the exact details and compatibility with ROS 2 Humble are not provided in the current search results.

1. **[differential_drive](http://wiki.ros.org/differential_drive)**: This package provides some basic tools for interfacing a differential-drive robot with the ROS navigation stack. It takes in a twist message from the navigation stack and provides left and right wheel messages to be used as motor driver strengths. However, this package is more focused on ROS 1 and might not be directly compatible with ROS 2.
    
2. **[diffdrive_arduino](http://wiki.ros.org/diffdrive_arduino)**: This package provides an interface between `ros_control` (specifically `diff_drive_controller`) and `ros_arduino_bridge`. It allows you to control your differential drive robot using an Arduino. This package is also more aligned with ROS 1 but could potentially be ported to ROS 2.

### What is `ros_control`?

`ros_control` is a framework for implementing and managing robot controllers in ROS (Robot Operating System). It provides a set of abstractions for hardware interfaces, controllers, and controller managers, making it easier to develop modular and reusable robot control software. The framework is commonly used for tasks like joint position control, velocity control, and trajectory following.

### URDF

### XACRO


ros2_control

static_transform_publisher

ros2 run tf2_ros static_transform_publisher x y z r p y parent_frame child_frame

foxglove

rviz2

tf2

rqt_tf_tree

ros2 run tf2_tools view_frames.py

ros2 pkg executables tf2_tools

`ros2 pkg executables tf2_tools`****

nohup rviz2 &

nohup rviz2 > output.log 2>&1 &

ps aux | grep rviz2

slam_toolbox

imu_filter_madgwick

pgrep -f ros2 | xargs kill -SIGINT

1280x720x6
256x144x90
480x270x15
480x270x30
480x270x6
480x270x60
640x360x30
640x480x15
640x480x30
640x480x6
848x480x10
848x480x6

### Simple test rtbmap

ros2 launch realsense2_camera rs_launch.py

ros2 run realsense2_camera realsense2_camera_node --ros-args -p enable_color:=false -p spatial_filter.enable:=true -p temporal_filter.enable:=true


Enabling accel and gyro is achieved either by adding the following parameters to the command line: ros2 launch realsense2_camera rs_launch.py pointcloud.enable:=true enable_gyro:=true enable_accel:=true or in runtime using the following commands:

ros2 param set /camera/camera enable_accel true
ros2 param set /camera/camera enable_gyro true

```shell
ros2 launch realsense2_camera rs_launch.py align_depth.enable:=true enable_sync:=true enable_accel:=true enable_gyro:=true unite_imu_method:=1 depth_module.profile:=640x480x30
```

```shell
ros2 run imu_filter_madgwick imu_filter_madgwick_node --ros-args -p use_mag:=false -r /imu/data_raw:=/camera/camera/imu
```

```bash
ros2 run tf2_ros static_transform_publisher 0.0 0.0 0.0 0.0 0.0 0.0 camera_imu_optical_frame camera_link
```

```shell
ros2 launch rtabmap_launch rtabmap.launch.py     rtabmap_args:="--delete_db_on_start --Optimizer/GravitySigma 0.3 "     rgb_topic:=/camera/camera/color/image_raw     depth_topic:=/camera/camera/aligned_depth_to_color/image_raw     camera_info_topic:=/camera/camera/color/camera_info     frame_id:=camera_link     approx_sync:=false     qos:=1     rviz:=true
```


this doesnt fucking works . any twist and odom is missed . 

	ros2 param set /camera/camera depth_module.emitter_enabled 0

	realsense-viewer

	rtav localization:=true