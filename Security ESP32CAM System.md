# Goal
from webcam record everyday on a different file. this files are accessible at address . is a webstie . that does not change. there is a player i can see this videos. also it shows Realtime . 
this system needs to store in chunks or something so that if power is lost stuff is still recorded. the recordings have timestamps

the computer is behind a router and there is no access to the router.

feauters 
- realtime 
- can see the recordings of an entire day
- can see the recordings of the day
- can see when the camera wasnt recording


## First Stage
- record from camera
- show Realtime
- make this accessible over the internet. 
- using free tools 

# Log
1. remote **ssh** to computer on the shopping center
	1. bore works
		1. does not want to connect to VSCODE
	2. simple bore the stream. 
		1. create bore connection from an unused port to something i can access.
		2. ssh local to reconnect ports 
		3. THIS WORKS 
		4. `bore local 8000 --to bore.pub`
		5. `ssh -L 8000:camera.local:81 localhost`
		6. this is good for testing but for the actual thing i will need a way to make local computer behind network to be publish a website available online 
		7. seems to make vscode work you just do the ssh connection many times. 
	2.  option
		1. reverse proxy
		2. vpn 
2. this work for the web. C:\Users\lukas>
3. 
```
npx lt --port 5000 --subdomain foxeyes
```

5. but i dont think it does for the ssh so lets find the simplest no installation one
https://github.com/anderspitman/awesome-tunneling?tab=readme-ov-file

install esp32cam libraries for both arduino and plataformio
https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/
```
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
```

```c++
#include "esp_camera.h"
#include <WiFi.h>
#include <ESPmDNS.h>

//
// WARNING!!! PSRAM IC required for UXGA resolution and high JPEG quality
//            Ensure ESP32 Wrover Module or other board with PSRAM is selected
//            Partial images will be transmitted if image exceeds buffer size
//
//            You must select partition scheme from the board menu that has at least 3MB APP space.
//            Face Recognition is DISABLED for ESP32 and ESP32-S2, because it takes up from 15 
//            seconds to process single frame. Face Detection is ENABLED if PSRAM is enabled as well

// ===================
// Select camera model
// ===================
//#define CAMERA_MODEL_WROVER_KIT // Has PSRAM
// #define CAMERA_MODEL_ESP_EYE // Has PSRAM
//#define CAMERA_MODEL_ESP32S3_EYE // Has PSRAM
//#define CAMERA_MODEL_M5STACK_PSRAM // Has PSRAM
//#define CAMERA_MODEL_M5STACK_V2_PSRAM // M5Camera version B Has PSRAM
//#define CAMERA_MODEL_M5STACK_WIDE // Has PSRAM
//#define CAMERA_MODEL_M5STACK_ESP32CAM // No PSRAM
//#define CAMERA_MODEL_M5STACK_UNITCAM // No PSRAM
#define CAMERA_MODEL_AI_THINKER // Has PSRAM
//#define CAMERA_MODEL_TTGO_T_JOURNAL // No PSRAM
//#define CAMERA_MODEL_XIAO_ESP32S3 // Has PSRAM
// ** Espressif Internal Boards **
//#define CAMERA_MODEL_ESP32_CAM_BOARD
//#define CAMERA_MODEL_ESP32S2_CAM_BOARD
//#define CAMERA_MODEL_ESP32S3_CAM_LCD
//#define CAMERA_MODEL_DFRobot_FireBeetle2_ESP32S3 // Has PSRAM
//#define CAMERA_MODEL_DFRobot_Romeo_ESP32S3 // Has PSRAM
#include "camera_pins.h"

// ===========================
// Enter your WiFi credentials
// ===========================
const char* ssid = "VICIO";
const char* password = "12345678";

void startCameraServer();
void setupLedFlash(int pin);

void setup() {
  Serial.begin(115200);
  Serial.setDebugOutput(true);
  Serial.println();

  camera_config_t config;
  config.ledc_channel = LEDC_CHANNEL_0;
  config.ledc_timer = LEDC_TIMER_0;
  config.pin_d0 = Y2_GPIO_NUM;
  config.pin_d1 = Y3_GPIO_NUM;
  config.pin_d2 = Y4_GPIO_NUM;
  config.pin_d3 = Y5_GPIO_NUM;
  config.pin_d4 = Y6_GPIO_NUM;
  config.pin_d5 = Y7_GPIO_NUM;
  config.pin_d6 = Y8_GPIO_NUM;
  config.pin_d7 = Y9_GPIO_NUM;
  config.pin_xclk = XCLK_GPIO_NUM;
  config.pin_pclk = PCLK_GPIO_NUM;
  config.pin_vsync = VSYNC_GPIO_NUM;
  config.pin_href = HREF_GPIO_NUM;
  config.pin_sccb_sda = SIOD_GPIO_NUM;
  config.pin_sccb_scl = SIOC_GPIO_NUM;
  config.pin_pwdn = PWDN_GPIO_NUM;
  config.pin_reset = RESET_GPIO_NUM;
  config.xclk_freq_hz = 20000000;
  config.frame_size = FRAMESIZE_UXGA;
  config.pixel_format = PIXFORMAT_JPEG; // for streaming
  //config.pixel_format = PIXFORMAT_RGB565; // for face detection/recognition
  config.grab_mode = CAMERA_GRAB_WHEN_EMPTY;
  config.fb_location = CAMERA_FB_IN_PSRAM;
  config.jpeg_quality = 12;
  config.fb_count = 1;
  
  // if PSRAM IC present, init with UXGA resolution and higher JPEG quality
  //                      for larger pre-allocated frame buffer.
  if(config.pixel_format == PIXFORMAT_JPEG){
    if(psramFound()){
      config.jpeg_quality = 10;
      config.fb_count = 2;
      config.grab_mode = CAMERA_GRAB_LATEST;
    } else {
      // Limit the frame size when PSRAM is not available
      config.frame_size = FRAMESIZE_SVGA;
      config.fb_location = CAMERA_FB_IN_DRAM;
    }
  } else {
    // Best option for face detection/recognition
    config.frame_size = FRAMESIZE_240X240;
#if CONFIG_IDF_TARGET_ESP32S3
    config.fb_count = 2;
#endif
  }

#if defined(CAMERA_MODEL_ESP_EYE)
  pinMode(13, INPUT_PULLUP);
  pinMode(14, INPUT_PULLUP);
#endif

  // camera init
  esp_err_t err = esp_camera_init(&config);
  if (err != ESP_OK) {
    Serial.printf("Camera init failed with error 0x%x", err);
    return;
  }

  sensor_t * s = esp_camera_sensor_get();
  // initial sensors are flipped vertically and colors are a bit saturated
  if (s->id.PID == OV3660_PID) {
    s->set_vflip(s, 1); // flip it back
    s->set_brightness(s, 1); // up the brightness just a bit
    s->set_saturation(s, -2); // lower the saturation
  }
  // drop down frame size for higher initial frame rate
  if(config.pixel_format == PIXFORMAT_JPEG){
    s->set_framesize(s, FRAMESIZE_QVGA);
  }

#if defined(CAMERA_MODEL_M5STACK_WIDE) || defined(CAMERA_MODEL_M5STACK_ESP32CAM)
  s->set_vflip(s, 1);
  s->set_hmirror(s, 1);
#endif

#if defined(CAMERA_MODEL_ESP32S3_EYE)
  s->set_vflip(s, 1);
#endif

// Setup LED FLash if LED pin is defined in camera_pins.h
#if defined(LED_GPIO_NUM)
  setupLedFlash(LED_GPIO_NUM);
#endif

  WiFi.begin(ssid, password);
  WiFi.setSleep(false);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected");

   if (!MDNS.begin("camera")) {
    Serial.println("Error setting up mDNS!");
    while (1) {
      delay(1000);
    }
  }
  Serial.println("mDNS responder started");

  // Add service to mDNS
  MDNS.addService("http", "tcp", 80);

  startCameraServer();

  Serial.print("Camera Ready! Use 'http://");
  Serial.print(WiFi.localIP());
  Serial.println("' to connect");
  Serial.print("Camera Ready! Use 'http://");
  Serial.print("camera.local");
  Serial.println("' to connect");
}

void loop() {
  // Do nothing. Everything is done in another task by the web server
  delay(10000);
}

```

ssh -L 8080:camera.local:81 localhost
npx lt --port 8080 --subdomain foxeyes
start /B "" pythonw app.py
start /B "" npx lt --port 5000 --subdomain foxeyes
This program functions as a comprehensive web-based surveillance system, aimed at capturing, recording, and streaming live video from a network-connected camera. It's structured to offer a seamless interface for users to monitor live feeds directly through a web browser. Additionally, the system supports video recording in segments, facilitating easy management and playback of footage. This setup is ideal for applications requiring continuous monitoring, such as in security, observational studies, or any scenario where remote visual monitoring is needed

powershell -Command "(Get-Item 'path\to\your\file.mp4').length / 1GB"

Get-ChildItem -File | Select-Object Name, @{Name='SizeInMB';Expression={"{0:N2}" -f ($_.Length / 1MB)}}

add . realtime viewing. add download day file. 