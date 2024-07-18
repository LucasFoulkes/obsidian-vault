Certainly! Below is a succinct tutorial on how to create a [[tmux]] session with specific panes running specified commands using a script named `movetest`.

1. **Create the Script**:
    - Open a text editor and create a file named `movetest.sh`.
    - Copy and paste the following code into `movetest.sh`:

```bash
#!/bin/bash

echo "Setting up ROS environment..."
echo "Sourcing global ROS setup file..."
source /opt/ros/humble/setup.bash

echo "Changing directory to ~/ros_ws..."
cd ~/ros_ws

echo "Sourcing local ROS setup file..."
source /opt/ros/humble/local_setup.bash

echo "Creating tmux session and starting ROS nodes..."
echo "Creating a new tmux session..."
tmux new-session -d -s ros_session

echo "Splitting the window into panes..."
tmux split-window -v

echo "Starting differential_bot node in the first pane..."
tmux send-keys -t ros_session:0.0 'source /opt/ros/humble/local_setup.bash && source install/setup.bash && ros2 run differential_bot differential_bot' C-m

echo "Starting teleop_twist_keyboard node in the second pane..."
tmux send-keys -t ros_session:0.1 'source /opt/ros/humble/local_setup.bash && source install/setup.bash && ros2 run teleop_twist_keyboard teleop_twist_keyboard' C-m

echo "Attaching to the tmux session..."
tmux attach -t ros_session

```

2. **Make the Script Executable**:
    - In the terminal, navigate to the directory containing `movetest.sh` and run:

```bash
chmod +x movetest.sh
```

3. **Move the Script to a Directory in Your PATH**:
    - Move `movetest.sh` to `/usr/local/bin` and rename it to `movetest`:

```bash
sudo mv movetest.sh /usr/local/bin/movetest
```

4. **Run Your Script**:
    - Now you can run `movetest` from the terminal to create your tmux session and start your ROS nodes:

```bash
movetest
```

This will create a tmux session named `ros_session`, split the window into two vertical panes, and run the specified ROS nodes in each pane.
this one is more verbose , becouse is boring to just see an empty terminal