## Using HC05 - cant be fucking used, maybe is clones fault
1. Program the HC05 
### Using an Arduino
We program the HC05 using  [[AT commands]]
1. Upload the following code to to the arduino
```C++
#include <SoftwareSerial.h>

#define rxPin 8
#define txPin 9

SoftwareSerial mySerial(rxPin, txPin);

char myChar;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("AT");

  mySerial.begin(38400);
  mySerial.println("AT");
}

void loop() {
  // put your main code here, to run repeatedly:
  while (mySerial.available()){
    myChar = mySerial.read();
    Serial.print(myChar);
  }

  while(Serial.available()){
    myChar = Serial.read();
    Serial.print(myChar);
    mySerial.print(myChar);
  }
}

```
for some reason this did work , used usb to ttl module
	1.  Enter the followin [[AT commands]], remember to use 38400 baud
```
AT+ORGL
AT+ROLE=0
AT+POLAR=1,0
AT+UART=115200,0,0
AT+INIT
```
3. Connect to computer over bluetooth.
- for some reason it does not work with windows 11, maybe all windows machines.
- Trying ubuntu
- It connects to ubuntu but then discontect in less than a second, will try diferent devices. 
- Diferent devices tried, will try diferent module. 
- Tried diferent HC05 module, same disconect after two seconds, fuck hc05
- Trying with hc10, also fucking invisible to win11. 
- Visible on ubuntu but not paring, trying diferent ubuntu computer
- New computer does not detect it , hc10 being a BLE device might be the reason
- hc10 even more of a bitch to detect, fuck.
- fuck hc10 and hc05, very much lets use ESP
- 20/10/22 trying again for last fucking time I guess
- simple recieving data 
1. fucking ubuntu binding
	1.  find out the mac address of the bluetooth device
	2. use ``` sudo rfcomm bind 0 [MAC ADDRESS] 1```
	3. use cutecom to connect it, is a bit hacky honestly
- simple data comunication did fucking work somehow yay
```
## Using HM10
## Using ESP
- ### Esp32
- ### Esp8266
## Using NRF24L01
```
- to connect to the bluettooth you need to use cutecom and is finiky
- 