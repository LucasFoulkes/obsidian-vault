**Introduction:** 
Welcome to the world of ROS 2 (Robot Operating System 2)! ROS 2 is a flexible framework for writing robot software. In ROS, the primary unit of execution is called a "node." Nodes are like small modular processes that perform specific tasks. They communicate using messages. In this tutorial, we'll create a "publisher" node that sends counting messages and a "subscriber" node that receives and displays them.

### **1. Setting up the Workspace and Package:**

Before we start, ensure you have ROS 2 installed on your system.

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```
*These commands set up a new workspace for our ROS 2 projects.*

```bash
ros2 pkg create --build-type ament_python my_py_pkg
```
*This command creates a new ROS 2 package named `my_py_pkg`.*

### **2. Crafting the Python Nodes:**

Navigate to our package directory and create two Python files:

```bash
cd my_py_pkg/my_py_pkg/
touch my_publisher.py my_subscriber.py
```

### **3. Penning the Publisher Node:**

Open `my_publisher.py` and add:

```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import Int32

class MyPublisher(Node):

    def __init__(self):
        super().__init__('my_publisher')
        self.publisher_ = self.create_publisher(Int32, 'count_topic', 10)
        self.timer_period = 1  # seconds
        self.timer = self.create_timer(self.timer_period, self.timer_callback)
        self.count = 0

    def timer_callback(self):
        msg = Int32()
        msg.data = self.count
        self.publisher_.publish(msg)
        self.get_logger().info(f'Publishing: "{msg.data}"')
        self.count += 1

def main(args=None):
    rclpy.init(args=args)
    node = MyPublisher()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### **4. Drafting the Subscriber Node:**

Open `my_subscriber.py` and add:

```python
import rclpy
from rclpy.node import Node
from std_msgs.msg import Int32

class MySubscriber(Node):

    def __init__(self):
        super().__init__('my_subscriber')
        self.subscription = self.create_subscription(
            Int32,
            'count_topic',
            self.listener_callback,
            10)

    def listener_callback(self, msg):
        self.get_logger().info(f'Received: "{msg.data}"')

def main(args=None):
    rclpy.init(args=args)
    node = MySubscriber()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

### **5. Directory Structure and Launch File:**

Your directory should resemble:

```
my_py_pkg/
│
├── my_py_pkg/
│   ├── __init__.py
│   ├── my_publisher.py
│   └── my_subscriber.py
│
├── launch/
│   └── my_launch_file.launch.xml
│
├── package.xml
├── resource/
│   └── my_py_pkg
├── setup.cfg
└── setup.py
```

In the `launch` directory, create an XML file named `my_launch_file.launch.xml`:

```xml
<launch>
    <node pkg="my_py_pkg" exec="my_publisher" name="my_publisher" />
    <node pkg="my_py_pkg" exec="my_subscriber" name="my_subscriber" />
</launch>
```

### **6. Adjusting the `setup.py` File and Building:**

Ensure the launch file is recognized during the build by modifying `setup.py` as previously provided.

Now, let's build our package and launch our nodes:

```bash
cd ~/ros2_ws
colcon build --symlink-install
source install/setup.bash
ros2 launch my_py_pkg my_launch_file.launch.xml
```

**Troubleshooting:**
- If you encounter any issues, ensure your directory structure matches the one provided.
- Double-check that you have all the necessary ROS 2 dependencies installed.
