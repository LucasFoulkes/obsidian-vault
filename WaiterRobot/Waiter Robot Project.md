# Overview
Develop a robot that navigates between points and recognizes markers but this is not required it also thru slam recoganized locations ,progressing through incremental phases.

## Hardware
- Raspberry pi 4 8g
- l298n motor controller
- d435i realsense depth camera
- power management 
- mobility/locomotion
## Phases

### 0: Hardware Design
- make it move, suspension and stuff. make sure everything is modular for experimentation, power management and stuff. 
### 1: Command-Line Control
- Enable basic robot movement via command-line instructions.

### 2: GUI Control (Optional)
- Develop an optional GUI for enhanced user-friendly robot control.

### 3: Dead Reckoning Feedback
- Implement positional feedback through dead reckoning techniques.

### 4: "To Goal" Behavior
- Enable autonomous navigation towards a specified goal.

### 5: SLAM Positioning
- Utilize D435i camera and sensors to implement SLAM for accurate robot positioning.

### 6: Enhanced "To Goal" Behavior
- Refine autonomous navigation utilizing SLAM data.

### 7: Behavior Definition Interface
- Create an interface for defining and adjusting robot behaviors.

---
# Command-Line Control

## Summary 
control the robot over comand line. setup ubuntu ros2 and arduino to work on the raspberry pi .  python node and arduino node. 

## Step 1: Setting Up the Environment

- **Objective:** Load Ubuntu 22.04 onto Raspberry Pi.
- **Action:** Loaded the ISO onto an SD card. Note: A detailed guide might be needed for beginners.
- **Objective:** Securely connect to the Raspberry Pi.
- **Action:** Used `ssh -X username@remote_host` to enable GUI viewing via SSH. No issues encountered.
- **Objective:** Get ROS Humble installed and configured.
- **Action:** Followed the [ROS2 Humble Installation](#) guide. Installation was straightforward.

## Step 2: Deciding on Robot Control Strategy

### Evaluating Control Methods
could connect rpi directly to l298n , but already have an arduino and why speend pins. maybe test later . it could cause a high voltage draw and reset the rpi. 

- **Objective:** Decide on a method for controlling the robot.
- **Decision:** Opted for "Rpi -> Arduino -> L298N" due to simplicity and immediate implementation.

## Step 3: Implementing the RPi Node

### Creating ROS Package and Node
- **Objective:** Set up the ROS package **waiter_bot** and node **arduino_bridge** .
- **Action:** Executed the following shell commands to create the package and node:
[[Creating and Launching a ROS 2 Python Package]]
###  Create node Arduino Bridge 
- **Initialize:** Set up serial communication with Arduino and subscribe to "cmd_vel".
- **Process Motion:** Extract linear and angular velocities, calculate wheel speeds, and send to Arduino.
- **Execute Movement:** Arduino receives speeds and controls the motors.
[[arduino_diff_controller]]

## Step 4: Testing the Node

### Running and Validating Nodes
- **Objective:** Test the `arduino_bridge` node and validate with `teleop_twist_keyboard`.
- **Action:** Ran nodes using the following commands and observed robot responses:
  ```shell
  ros2 run waiter_bot arduino_bridge
  ros2 run teleop_twist_keyboard teleop_twist_keyboard
  ```
- **Note:** Ensure the robot responds accurately to keyboard commands and adjust configurations as needed.

## Making Arduino program

1. install arduino on ubuntu
```bash
sudo apt install arduino
sudo usermod -a -G dialout $USER
```
2. make make sure ubuntu can connect to the usb and program the arduino run, should show you the gui over ssh 
```bash
nohup arduino &
```
3. the code , this is it in is  most basic for [[ArduinoDiffDrive]]

---
1. there is a buzzing this is caused by the pwm , 
	1. [x] fix by code 
this line did the magic. `  TCCR1B = (TCCR1B & 0b11111000) | 0b00000001; `
new code. improved. in the original document 

2. sometimes it randomy shutdowns when to much power to motor driver
- repeat issue to see when it happesn
	- happens with large value start, 
not sure if movement wich unplugs connections is the issue or is the sudden power changes
- first shake gently to see if cuases error
- shake harder
- do large speeds change without the robto moving the wheels lifter
- maybe the wheels need to have some force against them to have the issue happen repeat fast speed changes whith wheels , in traight line to prevent shacking
- identify couse 
- <mark>i will create a smothing node , if error persists then i will go back to finding the couse , maybe ask in some discord comunity</mark>

___
becouse i will be testing this a bunch i created a program to make it a single comand instead of like 10.  we will use alias [[Personalized Commands Linux]]]

---- 

## Smoothing Node
using this toprevent the rebooting problem
[[velocity_smoother]]

how to modify params in realtime.
1. Open `rqt`: `rqt`
2. Navigate to `Plugins` -> `Configuration` -> `Dynamic Reconfigure`
3. Select the `velocity_smoother` node and modify the parameters as needed.

or 

### Example Usage

Let's say you have a node named `velocity_smoother` and you want to change the `max_accel` parameter to `0.7`. You would run:

bashCopy code

`ros2 param set /velocity_smoother max_accel 0.7`

### Steps to Use `ros2 param set`

1. **List Running Nodes**: To see the list of running nodes, you can use the `ros2 node list` command.
    
    bashCopy code
    
    `ros2 node list`
    
2. **List Parameters for a Node**: To see the list of parameters for a specific node, you can use the `ros2 param list` command.
    
    bashCopy code
    
    `ros2 param list /velocity_smoother`
    
3. **Set Parameter**: Use the `ros2 param set` command to set the parameter value.
    
    bashCopy code
    
    `ros2 param set /velocity_smoother max_accel 0.7`
    
4. **Verify Parameter Change**: To make sure the parameter has been updated, you can get its current value using the `ros2 param get` command.
    
    bashCopy code
    
    `ros2 param get /velocity_smoother max_accel`

when ussing ssh seems the nodes from ros2 can bleed over? the fuck

---
sudden shutdonw remains. connected it to a tv , gather that yes inded it reboots. the tv went black no additional feedback

the culprit seems to be high voltage/amper draw. i think voltage becouse increasing pwa is an increase in voltage... i think? 

1. commands smoothing. becouse is not so much if pwa is to high but if it reached fast
2. use a step down boost conventer.  5v 
3. capacistors and more electronics to protect , hope i  dont  have to do this. 
4. seems if you reduce the voltage to the motor controller if the you aproach the maximun pwm and the motors doesnt move. the reset happens.

---

# Localization

## Summary 

i want to know where the robot think it is , we will do this in two steps. 
1. dead reconing, or without any sensors for feedback
<mark>2. with sensors. slam i guess</mark>
ros gives many ways to do this. the first way is kind pointless if im thinking of eventually doing the second one. but might be good for some learning. perhaps to save time lest just jump to the second one
1. make the d435i connect to ros2
2. make that into a location?
### D435i 
right now i have this camera, eventually i need a method to use a cheaper and more available camera.
- find online the most common and avaiblae and witha future depth camera
https://github.com/IntelRealSense/realsense-ros/tree/ros2-development
```shell
sudo apt install ros-$ROS_DISTRO-librealsense2*
sudo apt install ros-$ROS_DISTRO-realsense2-*
sudo apt install ros-$ROS_DISTRO-rtabmap-ros
```
will try to get both fucking infra cameras will do a stupid stereo camera. 
. they worked after updating d435i firmware

this works on laptop not on raspberry pi 4. 
external power usb, this also didn not work . either is not a power problem or the external powered usb did not work properly. 
**test :** **a)** using new usb. **b)** try using ros1 
**proposed solution :** **a)** if new usb works perfect , **b)** if ros1 works fuck maybe i will have to use that with or without rosbridge . **c)** us a fucking laptop