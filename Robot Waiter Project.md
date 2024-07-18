# Robot Navigation Project

## Overview
The goal of this project is to develop a robot that navigates between points and recognizes markers, progressing through incremental phases. The robot will utilize SLAM for accurate positioning and incorporate a D435i RealSense depth camera for localization.

## Hardware
- Raspberry Pi 4 (8GB)
- L298N motor controller
- D435i RealSense depth camera
- Power management system
- Mobility/locomotion components

## Phases
1. Hardware Design
   - Design a modular and experimental setup
   - Implement power management
   - Make sure everything is modular for experimentation

2. Command-Line Control
   - Enable basic robot movement via command-line instructions

3. GUI Control (Optional)
   - Develop an optional GUI for enhanced user-friendly robot control

4. Dead Reckoning Feedback
   - Implement positional feedback through dead reckoning techniques

5. "To Goal" Behavior
   - Enable autonomous navigation towards a specified goal

6. SLAM Positioning
   - Utilize D435i camera and sensors to implement SLAM for accurate robot positioning

7. Enhanced "To Goal" Behavior
   - Refine autonomous navigation utilizing SLAM data

8. Behavior Definition Interface
   - Create an interface for defining and adjusting robot behaviors

## Command-Line Control

### Setting Up the Environment
- Load Ubuntu 22.04 onto Raspberry Pi
  - A detailed guide might be needed for beginners
- Securely connect to the Raspberry Pi using `ssh -X username@remote_host` to enable GUI viewing via SSH
- Install and configure ROS Humble following the [ROS2 Humble Installation](#) guide

### Deciding on Robot Control Strategy
- Evaluate control methods
  - Could connect RPi directly to L298N, but already have an Arduino (why spend pins, maybe test later)
  - Direct connection could cause a high voltage draw and reset the RPi
- Choose "RPi -> Arduino -> L298N" approach for simplicity and immediate implementation

### Implementing the RPi Node
- Create ROS package `waiter_bot` and node `arduino_bridge`
  - Execute shell commands to create the package and node (see [[Creating and Launching a ROS 2 Python Package]])
- Set up serial communication with Arduino and subscribe to "cmd_vel"
- Process motion commands:
  - Extract linear and angular velocities
  - Calculate wheel speeds
  - Send speeds to Arduino
- Arduino receives speeds and controls the motors (see [[arduino_diff_controller]])

### Testing the Node
- Run `arduino_bridge` node and validate with `teleop_twist_keyboard`
  ```shell
  ros2 run waiter_bot arduino_bridge
  ros2 run teleop_twist_keyboard teleop_twist_keyboard
  ```
- Ensure the robot responds accurately to keyboard commands and adjust configurations as needed

### Making Arduino Program
1. Install Arduino on Ubuntu
   ```bash
   sudo apt install arduino
   sudo usermod -a -G dialout $USER
   ```
2. Make sure Ubuntu can connect to the USB and program the Arduino
   ```bash
   nohup arduino &
   ```
3. Implement the Arduino code for differential drive control (see [[ArduinoDiffDrive]])

#### Issues and Solutions
1. Buzzing caused by PWM
   - Fix by adding the line: `TCCR1B = (TCCR1B & 0b11111000) | 0b00000001;`
2. Random shutdowns when too much power is drawn by the motor driver
   - Repeat the issue to identify the cause
   - Test various scenarios (gentle shaking, hard shaking, large speed changes, etc.)
   - Create a smoothing node to address the issue (see [[velocity_smoother]])

### Smoothing Node
- Implement a smoothing node to prevent rebooting problems
- Modify parameters in real-time using `ros2 param set`
  - Example: `ros2 param set /velocity_smoother max_accel 0.7`
- Use `rqt` to modify parameters dynamically:
  1. Open `rqt`: `rqt`
  2. Navigate to `Plugins` -> `Configuration` -> `Dynamic Reconfigure`
  3. Select the `velocity_smoother` node and modify the parameters as needed

#### Issues and Solutions
- Sudden shutdown remains, likely due to high voltage/ampere draw
  1. Implement command smoothing
  2. Use a step-down boost converter (5V)
  3. Consider capacitors and additional electronics for protection
  4. Reduce voltage to the motor controller if approaching maximum PWM and motors don't move

## Localization

### Dead Reckoning
- Implement localization without sensors for feedback

### SLAM with D435i
- Connect D435i camera to ROS2
  ```shell
  sudo apt install ros-$ROS_DISTRO-librealsense2*
  sudo apt install ros-$ROS_DISTRO-realsense2-*
  sudo apt install ros-$ROS_DISTRO-rtabmap-ros
  ```
- Utilize SLAM for accurate localization
- Explore alternative depth camera options for future use

#### Issues and Solutions
- D435i not working on Raspberry Pi 4
  - Test with a new USB cable
  - Try using ROS1 with or without rosbridge
  - Consider using a laptop as an alternative

## Research and Ideas

### ROS Packages and Tools
- `diffdrive_arduino`: Provides an interface between `ros_control` (specifically `diff_drive_controller`) and `ros_arduino_bridge`
- `differential_drive`: Provides basic tools for interfacing a differential-drive robot with the ROS navigation stack (more focused on ROS 1)
- `ros_control`: A framework for implementing and managing robot controllers in ROS
- URDF (Unified Robot Description Format)
- Xacro (XML Macros for Robot Description Format)
- `ros2_control`
- `static_transform_publisher`
- Foxglove
- Rviz2
- TF2
- `rqt_tf_tree`
- `ros2 run tf2_tools view_frames.py`
- SLAM Toolbox
- `imu_filter_madgwick`

### Other Notes
- Test RTABmap with RealSense camera
  ```shell
  ros2 launch realsense2_camera rs_launch.py
  ros2 run realsense2_camera realsense2_camera_node --ros-args -p enable_color:=false -p spatial_filter.enable:=true -p temporal_filter.enable:=true
  ```
- Enable accel and gyro for RealSense camera
  ```shell
  ros2 param set /camera/camera enable_accel true
  ros2 param set /camera/camera enable_gyro true
  ```
- Launch RealSense camera with specific parameters
  ```shell
  ros2 launch realsense2_camera rs_launch.py align_depth.enable:=true enable_sync:=true enable_accel:=true enable_gyro:=true unite_imu_method:=1 depth_module.profile:=640x480x30
  ```
- Use `imu_filter_madgwick` for IMU filtering
  ```shell
  ros2 run imu_filter_madgwick imu_filter_madgwick_node --ros-args -p use_mag:=false -r /imu/data_raw:=/camera/camera/imu
  ```
- Publish static transform for the camera
  ```shell
  ros2 run tf2_ros static_transform_publisher 0.0 0.0 0.0 0.0 0.0 0.0 camera_imu_optical_frame camera_link
  ```
- Launch RTABmap with specific parameters
  ```shell
  ros2 launch rtabmap_launch rtabmap.launch.py rtabmap_args:="--delete_db_on_start --Optimizer/GravitySigma 0.3" rgb_topic:=/camera/camera/color/image_raw depth_topic:=/camera/camera/aligned_depth_to_color/image_raw camera_info_topic:=/camera/camera/color/camera_info frame_id:=camera_link approx_sync:=false qos:=1 rviz:=true
  ```