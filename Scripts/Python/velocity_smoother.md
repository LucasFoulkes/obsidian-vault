ros2 python node to smooth the twist messages , after having fix the sudden reset issue this is less necesary.
```python
import rclpy
from rclpy.node import Node
from geometry_msgs.msg import Twist
import threading
from rcl_interfaces.msg import ParameterEvent


class VelocitySmoother(Node):
    def __init__(self):
        super().__init__("velocity_smoother")
        self.declare_parameter("max_accel", 0.25)
        self.declare_parameter("dt", 0.015)
        self.target_linear_speed = 0.0
        self.target_angular_speed = 0.0
        self.current_linear_command = 0.0
        self.current_angular_command = 0.0
        self.max_accel = float(self.get_parameter("max_accel").value)
        self.dt = float(self.get_parameter("dt").value)
        self.lock = threading.Lock()
        self.subscription = self.create_subscription(
            Twist, "cmd_vel", self.listener_callback, 10
        )
        self.publisher = self.create_publisher(Twist, "cmd_vel_smoothed", 10)
        self.create_subscription(
            ParameterEvent, "/parameter_events", self.parameter_callback, 10
        )
        self.timer = self.create_timer(self.dt, self.update_speeds)

    def parameter_callback(self, msg):
        for param in msg.changed_parameters:
            if param.name == "max_accel":
                self.max_accel = float(param.value.double_value)
            elif param.name == "dt":
                self.dt = float(param.value.double_value)

    def listener_callback(self, msg):
        with self.lock:
            self.target_linear_speed = msg.linear.x
            self.target_angular_speed = msg.angular.z

    def update_speeds(self):
        with self.lock:
            # Update linear speed
            linear_diff = self.target_linear_speed - self.current_linear_command
            linear_accel = min(self.max_accel, abs(linear_diff) / self.dt)
            self.current_linear_command += (
                linear_accel * self.dt * (1 if linear_diff > 0 else -1)
            )

            # Update angular speed
            angular_diff = self.target_angular_speed - self.current_angular_command
            angular_accel = min(self.max_accel, abs(angular_diff) / self.dt)
            self.current_angular_command += (
                angular_accel * self.dt * (1 if angular_diff > 0 else -1)
            )

            # Publish smoothed command
            smoothed_msg = Twist()
            smoothed_msg.linear.x = self.current_linear_command
            smoothed_msg.angular.z = self.current_angular_command
            self.publisher.publish(smoothed_msg)


def main(args=None):
    rclpy.init(args=args)
    velocity_smoother = VelocitySmoother()
    rclpy.spin(velocity_smoother)
    velocity_smoother.destroy_node()
    rclpy.shutdown()


if __name__ == "__main__":
    main()
```