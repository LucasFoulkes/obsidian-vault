Arduino program to control two motors of a differential robot
```c++
const int BAUD_RATE = 9600;
const int MAX_SPEED_VALUE = 255;
const int BUFFER_SIZE = 32;

// Arduino motor pins
const int leftMotorSpeedPin = 9;  // Ensure these are PWM-capable pins
const int leftMotorDirPin1 = 7;
const int leftMotorDirPin2 = 8;

const int rightMotorSpeedPin = 10;  // Ensure these are PWM-capable pins
const int rightMotorDirPin1 = 5;
const int rightMotorDirPin2 = 6;

// Buffer to hold incoming data
char inputBuffer[BUFFER_SIZE];
int inputIndex = 0;

void setup() {
  // Initialize serial communication
  Serial.begin(BAUD_RATE);
  
  // Initialize motor pins as output
  initializeMotorPins();
  
  // Set the PWM frequency for pins 9 and 10 to 31.25 kHz
  // This frequency is chosen to reduce audible motor whine
  setPWMFrequency();
}

void loop() {
  // Read from serial port
  readSerialInput();
}

void initializeMotorPins() {
  pinMode(leftMotorSpeedPin, OUTPUT);
  pinMode(leftMotorDirPin1, OUTPUT);
  pinMode(leftMotorDirPin2, OUTPUT);
  
  pinMode(rightMotorSpeedPin, OUTPUT);
  pinMode(rightMotorDirPin1, OUTPUT);
  pinMode(rightMotorDirPin2, OUTPUT);
}

void setPWMFrequency() {
  TCCR1B = (TCCR1B & 0b11111000) | 0b00000001;
}

void readSerialInput() {
  while (Serial.available() > 0 && inputIndex < BUFFER_SIZE - 1) {
    char inChar = (char)Serial.read();
    inputBuffer[inputIndex++] = inChar;
    if (inChar == '\n') {
      inputBuffer[inputIndex] = '\0';  // Null-terminate the string
      processInput(inputBuffer);
      inputIndex = 0;  // Reset index for next input
    }
  }
}

void processInput(char* input) {
  if (input == NULL) {
    return;  // Return early if input is null
  }
  
  char* token = strtok(input, ",");
  if (token != NULL) {
    int left_speed = constrain(atoi(token), -MAX_SPEED_VALUE, MAX_SPEED_VALUE);
    token = strtok(NULL, ",");
    if (token != NULL) {
      int right_speed = constrain(atoi(token), -MAX_SPEED_VALUE, MAX_SPEED_VALUE);
      controlMotor(leftMotorSpeedPin, leftMotorDirPin1, leftMotorDirPin2, left_speed);
      controlMotor(rightMotorSpeedPin, rightMotorDirPin1, rightMotorDirPin2, right_speed);
    }
  }
}

void controlMotor(int speedPin, int dirPin1, int dirPin2, int speed) {
  if (speed > 0) {
    digitalWrite(dirPin1, HIGH);
    digitalWrite(dirPin2, LOW);
  } else if (speed < 0) {
    digitalWrite(dirPin1, LOW);
    digitalWrite(dirPin2, HIGH);
    speed = -speed;  // Make speed positive for PWM
  } else {
    digitalWrite(dirPin1, LOW);
    digitalWrite(dirPin2, LOW);
  }
  
  // Ensure speed is within limits for analogWrite
  speed = constrain(speed, 0, MAX_SPEED_VALUE);
  
  analogWrite(speedPin, speed);
}

```