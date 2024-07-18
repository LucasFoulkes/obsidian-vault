# Mathematical Model for a Differential Drive Robot

The mathematical model for a differential drive robot consists of several equations that describe the relationship between the motion of the robot's wheels and the resulting motion of the robot's center of mass. Here are the equations for the model:

## Kinematic Equations:

Linear velocity of the robot's center of mass ($V$):
$V = \frac{V_r + V_l}{2}$
where $V_r$ and $V_l$ are the velocities of the right and left wheels, respectively.
Angular velocity of the robot ($\omega$):
$\omega = \frac{V_r - V_l}{L}$
where $L$ is the distance between the wheels.

## Wheel Speed Equations:

Left wheel speed ($V_l$):
$V_l = V - \frac{\omega L}{2}$
Right wheel speed ($V_r$):
$V_r = V + \frac{\omega L}{2}$

where $V$ is the linear velocity of the robot's center of mass.

## Odometry Equations:

Odometry equation for x position:
$x(t + \Delta t) = x(t) + V(t) \Delta t \cos(\theta(t))$
Odometry equation for y position:
$y(t + \Delta t) = y(t) + V(t) \Delta t \sin(\theta(t))$
Odometry equation for orientation:
$\theta(t + \Delta t) = \theta(t) + \omega(t) \Delta t$

where $x$ and $y$ are the coordinates of the robot's center of mass, $\theta$ is the orientation of the robot, $V$ is the linear velocity of the robot's center of mass, $\omega$ is the angular velocity of the robot, and $\Delta t$ is the time step. These equations describe the motion of the robot based on the velocities of its wheels.

These equations are used extensively in robotics applications such as motion planning and control, but they make simplifying assumptions and may not fully capture the complex dynamics of a real-world robot. As a result, additional modeling and control techniques may be necessary to account for factors such as wheel slippage, terrain irregularities, and other sources of error.