# Smart Irrigation System using Arduino 🌱

This project automates the process of watering plants based on real-time soil moisture readings. Ideal for agriculture, gardening, and water conservation efforts.

## 💡 Features
- Detects soil moisture level in real-time
- Automatically activates water pump if soil is dry
- Energy-efficient, suitable for remote installations
- Can be expanded with IoT modules (e.g., ESP32 for remote monitoring)

## 🔧 Tools & Components
- Arduino UNO
- Soil Moisture Sensor
- Relay Module
- Water Pump / Motor
- Power Supply
- Jumper Wires, Breadboard

## 🧠 Code Overview
## 🧠 Code (with LCD Display)
```cpp
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,16,4);  // 16x2 LCD I2C address

void setup() {
  Serial.begin(9600);
  pinMode(2, OUTPUT);
  
  lcd.init(); lcd.clear(); lcd.backlight(); lcd.begin(16,2);
  lcd.setCursor(0,0); lcd.print("IRRIGATION");
  lcd.setCursor(0,1); lcd.print("SYSTEM IS ON ");
  delay(3000);
  lcd.clear();
}

void loop() {
  int value = analogRead(A0);
  Serial.println(value);

  if (value > 950) {
    digitalWrite(2, LOW); // Turn ON pump
    lcd.setCursor(0, 0); lcd.print("Pump is ON ");
  } else {
    digitalWrite(2, HIGH); // Turn OFF pump
    lcd.setCursor(0, 0); lcd.print("Pump is OFF");
  }

  // Display Moisture Level
  lcd.setCursor(0, 1);
  if (value < 350)
    lcd.print("Moisture:High");
  else if (value < 950)
    lcd.print("Moisture:Med ");
  else
    lcd.print("Moisture:Low ");
    
  delay(1000);
}
