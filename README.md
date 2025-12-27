# ESP32
<details>
  <summary>Arduino IDE Settings for ESP32-S3 N16R8</summary>
  <ul>
    <li>Select ESP32S3 Dev Module</li>
    <li>Change Flash Size to 16 MB</li>
    <li>Set to 16MB Flash (3MB APP/9.9MB FATFS)</li>
    <li>Set to OPI PSRAM (for Octal SPI PSRAM)</li>
    <li>Set Upload Speed to 921600</li>
    <li>Set to Hardware CDC and JTAG and USB CDC On Boot to Enabled (for USB programming)</li>
  </ul>
</details>
<details>
  <summary>Wifi Code Privat Network</summary>
  
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
```

</details>
<details>
  <summary>Wifi Code for Hotel Wifi</summary>

  ```c
#include <WiFi.h>
#include <esp_wifi.h>
  
// 1. Enter the MAC address of the device (Phone/Laptop) you used to login
//    Format: {0x00, 0x00, 0x00, 0x00, 0x00, 0x00}
uint8_t newMACAddress[] = {0xAC, 0x12, 0x34, 0x56, 0x78, 0x9A};  
const char* ssid = "Hotel_WiFi_Name";
const char* password = ""; // Usually empty for open portal networks
  
void setup() {
  Serial.begin(115200);
  // 2. Set WiFi mode to Station BEFORE changing MAC
  WiFi.mode(WIFI_STA);
  // 3. Spoof the MAC address
  esp_wifi_set_mac(WIFI_IF_STA, &newMACAddress[0]);
  // 4. Connect
  WiFi.begin(ssid, password);
  Serial.print("Connecting to Hotel WiFi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nConnected! Portal bypassed.");
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());
}
  
void loop() {
  // Your code here
}
```

</details>
<details>
  <summary>T-Embed C1101 Display Example</summary>

  ```c
#include "TFT_eSPI.h" 

// LORA
#define BOARD_LORA_CS   12
// TF card
#define BOARD_SD_CS   13

// About LCD definition in the file: lib/TFT_eSPI/User_Setups/Setup214_LilyGo_T_Embed_PN532.h
TFT_eSPI tft;

void setup(void)
{
    // LORA、SD and LCD use the same spi, in order to avoid mutual influence; 
    // before powering on, all CS signals should be pulled high and in an unselected state;
    pinMode(TFT_CS, OUTPUT);
    digitalWrite(TFT_CS, HIGH);
    pinMode(BOARD_SD_CS, OUTPUT);
    digitalWrite(BOARD_SD_CS, HIGH);
    pinMode(BOARD_LORA_CS, OUTPUT);
    digitalWrite(BOARD_LORA_CS, HIGH);
    
    tft.begin();
    tft.setRotation(3);
    tft.fillScreen(TFT_BLACK);

}

void loop(void)
{
    tft.fillScreen(TFT_RED);
    delay(1000);
    tft.fillScreen(TFT_GREEN);
    delay(1000);
    tft.fillScreen(TFT_BLUE);
    delay(1000);
    tft.fillScreen(TFT_LIGHTGREY);
    delay(1000);
    tft.fillScreen(TFT_BLACK);
    delay(1000);

    tft.setTextColor(TFT_GREEN, TFT_BLACK);
    tft.setRotation(3);
    tft.drawString(" !\"#$%&'()*+,-./0123456", 0, 0, 2);
    tft.drawString("789:;<=>?@ABCDEFGHIJKL", 0, 16, 2);
    tft.drawString("MNOPQRSTUVWXYZ[\\]^_`", 0, 32, 2);
    tft.drawString("abcdefghijklmnopqrstuvw", 0, 48, 2);
    delay(1000);

    tft.setRotation(2);
    tft.fillScreen(TFT_BLACK);
    tft.drawString(" !\"#$%&'()*+,-./0123456", 0, 0, 2);
    tft.drawString("789:;<=>?@ABCDEFGHIJKL", 0, 16, 2);
    tft.drawString("MNOPQRSTUVWXYZ[\\]^_`", 0, 32, 2);
    tft.drawString("abcdefghijklmnopqrstuvw", 0, 48, 2);
    delay(1000);

    tft.setRotation(1);
    tft.fillScreen(TFT_BLACK);
    tft.drawString(" !\"#$%&'()*+,-./0123456", 0, 0, 2);
    tft.drawString("789:;<=>?@ABCDEFGHIJKL", 0, 16, 2);
    tft.drawString("MNOPQRSTUVWXYZ[\\]^_`", 0, 32, 2);
    tft.drawString("abcdefghijklmnopqrstuvw", 0, 48, 2);
    delay(1000);

    tft.setRotation(0);
    tft.fillScreen(TFT_BLACK);
    tft.drawString(" !\"#$%&'()*+,-./0123456", 0, 0, 2);
    tft.drawString("789:;<=>?@ABCDEFGHIJKL", 0, 16, 2);
    tft.drawString("MNOPQRSTUVWXYZ[\\]^_`", 0, 32, 2);
    tft.drawString("abcdefghijklmnopqrstuvw", 0, 48, 2);
    delay(1000);
}
```
</details>
