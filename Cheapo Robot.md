# Goal 
Make a robot(robot base) that is easy and cheap to make. Should work as a platform or test to make other robots. 
Like Legos and sandwich like you can stack the architecture to give space to add more components. 
first stage is just the physical design of it the style mechanism by which the basic base is and then how new components can be added and also like be part of that design concept. 
Maybe it could be like a course on robotics and this a base?
**Breadboard**
1. photovore one sensor
types of behaviours from this. 
detects lights move forward , threshold . function of light to power ( cant do motor speed becouse like how do i even read that )
2. photovore 2 sensors
same but with two sensors. so like 
4. photovore 2 sensors switch obstacle avoidance
5. Learning about H Bridge
6. analogic
7. digital
8. using motor controller
9. wall following
10. line following
**Arduino**
1. random walk 
2. random walk obstacle avoidance
3. random walk photovore
4. remote control
5. wall following
6. light following
7. light following but the line has information that leads the robot to do other stuff
8. ultrasonic sensor
**Advanced**
1. OTA using Bluetooth
2. OTA using ESP8266
3. <mark>Braitenberg Vehicles</mark>
4. Directional Audio
5. camera for recording and streaming so like a guardian 
6. as ros2 peripheral
7. solar charging
a tool?
test basic robots to sell
test advanced odometry stuff to accomplish something.
Roomba. 

---
# Log
arduino
```c++
void setup() {
  // Initialize serial communication at 115200 baud
  Serial.begin(115200);
}

void loop() {
  // Read the value from analog pin A5
  int sensorValue = analogRead(A5);

  // Send the sensor value to the serial port
  Serial.println(sensorValue);

  // Delay for a short period
  delay(10);
}
```
python
```python
import socket
import threading
import pygame
from queue import Queue
from collections import deque

# ESP-01 IP and Port
ESP_IP = '192.168.1.104'  # Replace with your ESP-01's IP address
ESP_PORT = 23  # Default port for esp-link

# Create a TCP socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
    client_socket.connect((ESP_IP, ESP_PORT))
    print(f"Connected to {ESP_IP} on port {ESP_PORT}")
except socket.error as e:
    print(f"Unable to connect to {ESP_IP} on port {ESP_PORT}: {e}")
    exit(1)

data_queue = Queue()

def read_from_esp():
    while True:
        try:
            data = client_socket.recv(1024)
            if data:
                decoded_data = data.decode('utf-8').strip()
                for value in decoded_data.split('\n'):
                    if value:
                        print(value)
                        data_queue.put(value)
            else:
                break
        except socket.error as e:
            print(f"Error reading from socket: {e}")
            break

# Start the reading thread
read_thread = threading.Thread(target=read_from_esp)
read_thread.daemon = True
read_thread.start()

# Pygame setup
pygame.init()
window_size = (800, 600)
screen = pygame.display.set_mode(window_size)
pygame.display.set_caption('Real-time Data from ESP-01')

data = deque(maxlen=100)  # Use a deque with a maximum length
window_length = 100  # Number of data points to show in the window
running = True
clock = pygame.time.Clock()

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    while not data_queue.empty():
        new_data = data_queue.get()
        try:
            value = float(new_data)
            data.append(value)
        except ValueError:
            print(f"Invalid data format: {new_data}")
    
    screen.fill(WHITE)
    if len(data) > 1:
        points = [(window_size[0] - i * (window_size[0] / window_length), 
                   window_size[1] - (y / 1024) * window_size[1]) 
                  for i, y in enumerate(reversed(data))]
        pygame.draw.lines(screen, RED, False, points)

    pygame.display.flip()
    clock.tick(30)  # Limit the frame rate to 30 FPS

pygame.quit()
client_socket.close()
```
arduino
```c++
void setup() {
  // Initialize serial communication at 115200 baud
  Serial.begin(115200);
}

void loop() {
  // Initialize a counter
  static int counter = 0;

  // Send the counter value to the serial port
  Serial.println(counter);

  // Increment the counter
  counter++;

  delay(10);
}

```
python
```python
import socket
import threading

# ESP-01 IP and Port
ESP_IP = '192.168.1.104'  # Replace with your ESP-01's IP address
ESP_PORT = 23  # Default port for esp-link

# Create a TCP socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

try:
    client_socket.connect((ESP_IP, ESP_PORT))
    print(f"Connected to {ESP_IP} on port {ESP_PORT}")
except socket.error as e:
    print(f"Unable to connect to {ESP_IP} on port {ESP_PORT}: {e}")
    exit(1)

def read_from_esp():
    while True:
        try:
            data = client_socket.recv(1024)
            if data:
                print(data.decode('utf-8'), end='')
            else:
                break
        except socket.error as e:
            print(f"Error reading from socket: {e}")
            break

# Start the reading thread
read_thread = threading.Thread(target=read_from_esp)
read_thread.daemon = True
read_thread.start()

try:
    while True:
        message = input()
        client_socket.sendall(message.encode('utf-8'))
except KeyboardInterrupt:
    print("Exiting...")
finally:
    client_socket.close()

```
https://www.youtube.com/watch?v=mtazgora9xE&t=1267s
https://github.com/jeelabs/esp-link
```bash
com2tcp --baud 115200 --ignore-dsr \\.\CNCB0 192.168.0.249 23
```
**PWM Modulation**
- motors don't start 
- one motor is better than other one
**Attempt 1** 
- Ceramic Capacitors
**Result**
- 0.1 issue change motors now move but one motor only starts moving at much higher PWM than the other one. 
**Attempt 2**
- Change motor outputs to see if issue is motor
**Result**
- Issuer remains in the same motors. problem not pins it seems. 
**Attempt
- Change the motor itself.
**Result**
- motor is error 
**Attempt** 
- changed motor , this did help
**Pending Issues**
- OTA for the arduino using esp8266 requires phisical reset 
- the fact that im using esp8266 bluetooth would be more seamless
- the motor buzzing 
- the odometry
---
```
robot.moveByMotor(leftmotorvelocity,rightmotorvelocity)
```
```
robot.move(angularvelocity,angularspeed)
```
```
robot.leftmotor(velocity)
```

if timestep
robot.leftmotor(randomvalue)
robot.rightmotor(randomvalue)
new timestep

12/6/2024
machine learning algorithm to learn ... using mpu9060 and maybe the magnetic compass.  
1. odometry 
2. + ultrasonic sensor to learn to avoid objects. 
3. + solar panel , goal to explore environment but remain charged. to patrol , clean  