### Components para projecto
https://megatronica.cc/producto/conector-db25-hembra-para-cable-25-pines/
https://megatronica.cc/producto/molex-6-pines-con-cable-jstxh2-54/
https://megatronica.cc/producto/molex-4-pines-kf2510-54/
https://megatronica.cc/producto/modulo-reloj-ds1307-con-pila-2032-arduino/
https://megatronica.cc/producto/sensor-turbidez-agua-analogo-acondicionamiento/
https://megatronica.cc/producto/sensor-de-calidad-de-agua-tds-driver-arduino/
https://megatronica.cc/producto/modulo-sensor-detector-humedad-agua-lluvia-para-arduino/
https://megatronica.cc/producto/sensor-capacitivo-de-humedad-del-suelo/
seems ground sensors are quite terrible there are youtube videos about it. 
https://megatronica.cc/producto/sensor-de-temperatura-de-termistor-ntc/
https://megatronica.cc/producto/valvula-solenoide-electrovalvula-12vdc/
https://megatronica.cc/producto/sensor-de-flujo-de-agua-1-2/
https://megatronica.cc/producto/conector-para-chasis-de-4-salidas-de-parlante/
https://megatronica.cc/producto/socket-electrico-4p-con-cables/
https://megatronica.cc/producto/conector-xt60-hembra/
https://megatronica.cc/producto/modulo-cargador-solar-para-bateria-de-litio-cn3065/
https://megatronica.cc/producto/panel-solar-celda-5v-180ma-107x62/
https://megatronica.cc/producto/sensor-uv-de-intensidad-de-rayos-ultravioleta-de-luz-solar/
https://megatronica.cc/producto/modulo-de-control-de-carga-de-bateria-12v-24v-xh-m603/
https://megatronica.cc/producto/ads1115-convertidor-analogico-digital/
https://roboticsec.com/producto/modulo-convertidor-analogico-digital-ads1115-iic-i2c/
https://articulo.mercadolibre.com.ec/MEC-517784162-conector-db37-pines-para-soldar-_JM#polycard_client=search-nordic&position=1&search_layout=stack&type=item&tracking_id=9331bf41-785b-4035-a6c3-66ca82fe423a
https://articulo.mercadolibre.com.ec/MEC-566503380-wago-borna-de-conexion-5-conductores-6mm-compact-_JM#polycard_client=search-nordic&position=1&search_layout=stack&type=item&tracking_id=c555d8a8-69f5-42dc-9a75-5d099369182a
https://articulo.mercadolibre.com.ec/MEC-566709528-wago-conector-en-linea-con-palancas-de-sujecion-_JM#polycard_client=search-nordic&position=11&search_layout=stack&type=item&tracking_id=c555d8a8-69f5-42dc-9a75-5d099369182a
https://articulo.mercadolibre.com.ec/MEC-601069914-conectores-rapidos-tipo-wago-de-varios-pines-_JM#polycard_client=search-nordic&position=12&search_layout=stack&type=item&tracking_id=c555d8a8-69f5-42dc-9a75-5d099369182a
https://www.cineto.net/producto/conector-db37-pines-para-soldar/
https://grupoelectrostore.com/shop/displays-y-pantallas/modulo-pantalla-28-tft-touch-spi-tft/
me gusta esta pantalla
https://www.altayerengineering.com/products/installation-connectors-gesis-classic-gst-connector-installation-systems-indoor/
https://grupoelectrostore.com/shop/modulos-y-shields/modulo-ads1115-16-bitsadc-4-canales/
https://roboticsec.com/producto/pantalla-touch-tft-2-8-spi-240x320/
https://roboticsec.com/producto/pantalla-touch-tft-3-5-320x480/
https://avelectronics.cc/producto/convertidor-analogo-digital-ads1115-4-canales-16-bit/?srsltid=AfmBOooScm8-7X0UtLO7iXGhsi7cJnsLpuD4nl5gN0Mo2xjalS6Gq7rm
https://avelectronics.cc/producto/mcp3208-ci-sl/?srsltid=AfmBOor1lZIcWyRrAwX2f9dukM0A7PLskwr4bGmPtlFD7ph05b14LYqO
https://avelectronics.cc/producto/tft-3-2-touch-screen-shield-for-arduino-uno-mega/
https://avelectronics.cc/producto/3-5-tft-touch-for-raspberry-pi-2-3/

# 1. Required Libraries

- **TFT_eSPI** by Bodmer  
    (Install via Arduino Library Manager or from GitHub: [Bodmer/TFT_eSPI](https://github.com/Bodmer/TFT_eSPI))
    
- **XPT2046_Touchscreen** by Paul Stoffregen  
    (Install via Arduino Library Manager or from GitHub: [PaulStoffregen/XPT2046_Touchscreen](https://github.com/PaulStoffregen/XPT2046_Touchscreen))

# 2. Hardware Connections

## TFT Display (Using VSPI as set in TFT_eSPI User_Setup.h)

| **Signal** | **ESP32 Pin** | **Description**                                   |
| ---------- | ------------- | ------------------------------------------------- |
| TFT_MOSI   | GPIO23        | Data input for TFT display                        |
| TFT_SCLK   | GPIO18        | Clock for TFT display                             |
| TFT_MISO   | GPIO19        | (Optional – often unused for write-only displays) |
| TFT_CS     | GPIO15        | Chip select for TFT display                       |
| TFT_DC     | GPIO2         | Data/Command control                              |
| TFT_RST    | GPIO4         | Reset pin (or -1 if tied to ESP32 reset)          |
| TFT_BL     | (Optional)    | Backlight control (if applicable)                 |
## Touch Controller (Using dedicated HSPI)

| **Signal** | **ESP32 Pin** | **Description**                                    |
| ---------- | ------------- | -------------------------------------------------- |
| TOUCH_MOSI | GPIO13 (DIN)  | Data input for touch controller                    |
| TOUCH_SCLK | GPIO14        | Clock for touch controller                         |
| TOUCH_MISO | GPIO12 (DO)   | Data output from touch controller                  |
| TOUCH_CS   | GPIO5         | Chip select for touch controller                   |
| TOUCH_IRQ  | GPIO16        | Not used here (set to 255 in software if not used) |
## Common Connections

| **Connection** | **Notes**                               |
| -------------- | --------------------------------------- |
| VCC            | Supply voltage as per your module specs |
| GND            | All modules must share a common ground  |

# 3. File Editing

there is a file **User_Setup.h** fzf then User_setup.h to find it. then find the line  `// ###### EDIT THE PIN NUMBERS IN THE LINES FOLLOWING TO SUIT YOUR ESP32 SETUP   ######`
edit the pint alocation below it. 

# 4 Code
## Test Touch

```c
#include <SPI.h>
#include <XPT2046_Touchscreen.h>

// Define the touchscreen pins
#define TOUCH_MOSI 13   // Data input for touch controller (DIN)
#define TOUCH_SCLK 14   // Clock for touch controller (SCLK)
#define TOUCH_MISO 12   // Data output from touch controller (DO)
#define TOUCH_CS   5    // Chip select for touch controller
#define TOUCH_IRQ  4    // Touch interrupt pin (use 255 if not used)

// Create a dedicated SPI instance for the touch controller (using HSPI)
SPIClass touchSPI(HSPI);

// Instantiate the touchscreen object with chip select and IRQ.
XPT2046_Touchscreen ts(TOUCH_CS, TOUCH_IRQ);

void setup() {
  Serial.begin(115200);
  while (!Serial) { } // Wait for Serial

  // Initialize the dedicated SPI bus for the touchscreen with the defined pins.
  touchSPI.begin(TOUCH_SCLK, TOUCH_MISO, TOUCH_MOSI, TOUCH_CS);

  // Initialize the touchscreen using the dedicated SPI instance.
  ts.begin(touchSPI);
  ts.setRotation(1);  // Adjust rotation as needed

  Serial.println("Touch test started. Touch the screen to see raw output.");
}

void loop() {
  // Check if the touchscreen is touched.
  if (ts.touched()) {
    TS_Point p = ts.getPoint();
    Serial.print("Touch detected: X = ");
    Serial.print(p.x);
    Serial.print(", Y = ");
    Serial.print(p.y);
    Serial.print(", Pressure = ");
    Serial.println(p.z);
  }
  delay(50);  // Small delay to reduce serial output spam
}

```

