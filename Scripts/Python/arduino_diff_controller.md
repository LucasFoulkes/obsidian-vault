```python
#!/usr/bin/env python3
import rclpy
from rclpy.node import Node
from geometry_msgs.msg import Twist
import serial


class DifferentialBot(Node):O
    # Class variables for robot parameters
    WHEEL_RADIUS_LEFT = 0.1  # Left wheel radius in meters
    WHEEL_RADIUS_RIGHT = 0.1  # Right wheel radius in meters
    WHEEL_DISTANCE = 0.5  # Distance between wheels in meters
    CORRECTION_FACTOR_LEFT = 1.0  # default is 1.0 (no correction)
    CORRECTION_FACTOR_RIGHT = 1.0  # default is 1.0 (no correction)
    QUEUE_SIZE = 10  # Queue size for subscription

    def __init__(self, serial_port="/dev/ttyACM0", baud_rate=9600):
        super().__init__("differential_bot")

        # Initialize serial connection
        try:
            self.ser = serial.Serial(serial_port, baud_rate)
            self.get_logger().info(f"Connected to {serial_port}")
        except serial.SerialException as e:
            self.get_logger().error(f"Failed to establish a serial connection: {e}")
            self.destroy_node()
            rclpy.shutdown()

        # Last command sent
        self.last_command = None

        # Subscribe to cmd_vel topic
        self.subscription = self.create_subscription(
            Twist, "cmd_vel", self.listener_callback, self.QUEUE_SIZE
        )

    def listener_callback(self, msg: Twist):
        """Callback function for cmd_vel subscription."""
        # Extract linear and angular velocity from the Twist message
        linear_vel = msg.linear.x
        angular_vel = msg.angular.z

        # Calculate individual wheel speeds
        left_wheel_speed, right_wheel_speed = self.calculate_wheel_speeds(
            linear_vel, angular_vel
        )

        # Send command to Arduino
        self.send_command_to_arduino(left_wheel_speed, right_wheel_speed)

    def calculate_wheel_speeds(self, linear_vel: float, angular_vel: float) -> tuple:
        """
        Calculate individual wheel speeds based on linear and angular velocity.

        :param linear_vel: Linear velocity from Twist message.
        :param angular_vel: Angular velocity from Twist message.
        :return: Tuple containing left and right wheel speeds.
        """
        # Based on global robot parameters
        left_wheel_speed = (
            linear_vel - angular_vel * self.WHEEL_DISTANCE / 2
        ) / self.WHEEL_RADIUS_LEFT
        right_wheel_speed = (
            linear_vel + angular_vel * self.WHEEL_DISTANCE / 2
        ) / self.WHEEL_RADIUS_RIGHT

        # Apply correction factors
        left_wheel_speed *= self.CORRECTION_FACTOR_LEFT
        right_wheel_speed *= self.CORRECTION_FACTOR_RIGHT

        return left_wheel_speed, right_wheel_speed

    def send_command_to_arduino(
        self, left_wheel_speed: float, right_wheel_speed: float
    ):
        """
        Send wheel speeds command to Arduino via serial communication.

        :param left_wheel_speed: Left wheel speed.
        :param right_wheel_speed: Right wheel speed.
        """
        # Convert wheel speeds to integers with higher resolution
        # Multiplication by 10 is for higher resolution in the Arduino
        left_wheel_speed_int = int(left_wheel_speed * 10)
        right_wheel_speed_int = int(right_wheel_speed * 10)

        # Convert wheel speeds to a string to send via serial
        command = f"{left_wheel_speed_int},{right_wheel_speed_int}"

        # Send the command to the Arduino only if it has changed
        if command != self.last_command:
            try:
                self.ser.write((command + "\n").encode("utf-8"))
                self.get_logger().info(
                    f"Sent speeds: {left_wheel_speed_int},{right_wheel_speed_int}"
                )
                self.last_command = command
            except serial.SerialException as e:
                self.get_logger().error(f"Failed to send command to Arduino: {e}")


def main(args=None):
    rclpy.init(args=args)
    node = DifferentialBot()
    rclpy.spin(node)


if __name__ == "__main__":
    main()
```