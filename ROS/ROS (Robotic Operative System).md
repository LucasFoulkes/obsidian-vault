[Target Distros ](https://www.ros.org/reps/rep-2000.html#galactic-geochelone-may-2021-november-2022)
## ROS2 / Foxy
### Installation
[source](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html)
```bash
locale  # check for UTF-8

sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings
```
```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```
```bash
sudo apt update && sudo apt install curl gnupg2 lsb-release
```
```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
```
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
```bash
sudo apt update
```
```bash
sudo apt upgrade
```
```bash
sudo apt install ros-foxy-desktop python3-argcomplete
```
- bare bones
```bash
sudo apt install ros-foxy-ros-base python3-argcomplete
```
```bash
sudo apt install ros-dev-tools
```
## Packages
are a way organize your programs, they exist inside of your worlplace.
a package is all the files that a specific ROS2 progam containts.
You can create a python package or a c+.
A python package will have.
- package.xml - file containing meta information.
- setup.py - file containing on how to compile the package.
- setup.cfg - file that define where the scripts will be installed.
- /<package_name> - this directory will always have the same name as your package , python files go inside.
Some packages might contain extra folders. For instance, the launch folder contains the package's launch files.
---
-   Every ROS2 program that you want to execute is organized in a package.
-   Every ROS2 program you create must be organized in a package.
-   Packages are the primary organization system for ROS2 programs.
---
## HOWTO Create a Package
1. Source ROS2.
```
source /opt/ros/galactic/setup.bash
```
2. Make/Already have a workspace. ==look into what workspace are==.
```
mkdir -p ros2_ws/src
```
```
cd ~/ros2_ws/
```
3. Create a package using ROS2.
```
cd src
```
```
ros2 pkg create --build-type ament_python my_package --dependencies rclpy
```
4. Build the package.
```
cd ~/ros2_ws/
```
```
colcon build
```
```
source install/setup.bash
```
If colcon build not found then
```
sudo apt install python3-colcon-common-extensions
```
5. Make the launch file executable

---	
Check all packages available.
``ros2 pkg list`` 
Only build one package
``colcon build --packages-select <package_name>``

---

## Launch file
```python
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        launch_ros.actions.Node(
            package='turtlebot3_teleop',
            executable='teleop_keyboard',
            output='screen'),
    ])
```
## HOWTO first ROS2 Program
1. Create a Package 
2. Inside the package you created inside the folder with the same name , along __int__.py create create the executable simple.py.
```python
import rclpy
# import the Node module from ROS2 Python library
from rclpy.node import Node

def main(args=None):
    # initialize the ROS communication
    rclpy.init(args=args)
    # print a message to the terminal
    print("Moe yo Byakugan! Kore ga watashi no nindō yo ")
    # Translated to English should be "Blaze Away, Byakugan! This is My Ninja Way!"
    # shutdown the ROS communication
    rclpy.shutdown()

if __name__ == '__main__':
    main() #call the main function
```
3. Inside src file create a launch folder and a launch file inside it.
```python 
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='my_package',
            executable='simple_node',
            output='screen'),
    ])
```
4. chmod +x launch_file.launch.py
4. modify setup file
```python
from setuptools import setup
import os
from glob import glob

package_name = 'my_package'

setup(
    name=package_name,
    version='0.0.0',
    packages=[package_name],
    data_files=[
        ('share/ament_index/resource_index/packages',
            ['resource/' + package_name]),
        ('share/' + package_name, ['package.xml']),
        (os.path.join('share', package_name), glob('launch/*.launch.py'))
    ],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='somebody very awesome',
    maintainer_email='user@user.com',
    description='TODO: Package description',
    license='TODO: License declaration',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            'simple_node = my_package.simple:main'
        ],
    },
)
```
5. from the workspace build the package and source it.
	1. ``cd ~/ros2_ws``
	2. ``colcon build --package-select my_package``
	3. ``source install/setup.bash``
6. run it.
	1. ``ros2 launch my_package my_package_launch_file.launch.py``
	
--- 
list all available nodes
``ros2 node list``

---

## Topics 

### Basic Topic Commands
-  ``ros2 topic -h``
- ``ros2 topic list``
- ``ros2 topic info /cmd_vel``
- The comand above will give you the following information
	- **Type:** Refers to the #ROS_Interface associated with the Topic with which you need to work with this Topic.
	- **Publisher count:** Refers to the number of active Publishers connected to the Topic.
	- **Subscription count:** Refers to the number of active Subscribers connected to the Topic.
- ``ros2 topic echo /cmd_vel``
	- The ros2 topic echo command is used to read (subscribe to) the published Topic. The command structure is as follows:
- ``ros2 interface list``
- The ros2 interface list command prints a list of all the available interfaces.
	- Messages: Can be found as .msg files. They are simple text files that describe the fields of a ROS message. You can use them to generate source code for messages.
	- Services: Can be found as .srv files. They are composed of two parts: a request and a response. Both are message declarations.
	- Actions: Can be found as .action files. They are composed of three parts: a goal, a result, and feedback. Each part contains a message declaration.
- ``ros2 interface proto <NAME OF INTERFACE>``
- ``ros2 topic pub /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.0}}"``
- ``ros2 topic info /cmd_vel``
- ``ros2 topic pub --once /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}``
- ``ros2 interface show sensor_msgs/msg/LaserScan``
- ``ros2 topic info /scan -v``
