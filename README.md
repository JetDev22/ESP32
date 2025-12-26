# ESP32

## Arduino IDE Settings for ESP32-S3 N16R8
- Select ESP32S3 Dev Module
- Change Flash Size to 16 MB
- Set to 16MB Flash (3MB APP/9.9MB FATFS)
- Set to OPI PSRAM (for Octal SPI PSRAM)
- Set Upload Speed to 921600
- Set to Hardware CDC and JTAG and USB CDC On Boot to Enabled (for USB programming)

## Wifi Code ESP32-S3
```
```
``` 
```c 
#include <WiFi.h>

const char* ssid = "Your_SSID";
const char* password = "Your_Password";

void setup() {
  Serial.begin(115200);
  WiFi.mode(WIFI_STA); // Set as Station mode
  WiFi.begin(ssid, password);
  
  Serial.print("Connecting to WiFi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nConnected!");
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  // Your application logic here
}```

## Next
