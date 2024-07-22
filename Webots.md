[source](https://cyberbotics.com/doc/guide/installation-procedure)
Robot simulation software

## Installation
```bash
wget -qO- https://cyberbotics.com/Cyberbotics.asc | sudo apt-key add -
```
```bash
sudo apt-add-repository 'deb https://cyberbotics.com/debian/ binary-amd64/' 
```
```bash
sudo apt-get update
```
```bash
sudo apt-get upgrade
```
```bash
sudo apt-get install webots
```

## Webots_ros2
[source](https://github.com/cyberbotics/webots_ros2)
1. 
```bash
sudo apt-get install ros-$ROS_DISTRO-webots-ros2
``` 