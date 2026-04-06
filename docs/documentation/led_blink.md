# Arduino and Liquid Crystal Display (LCD)

Here's a beginner-friendly Arduino LCD Reference Manual that introduces both 16-pin standard LCDs and 4-pin I2C LCDs using Arduino UNO. This is written with the assumption that students are just getting started, so it includes relevant terminologies and suggested keywords for further research.


## Blink code for arduino

you can test the defualt blink code in arduino under file tab.

<img src="https://fabacademy.org/2025/labs/dgi/students/tsheyang-tshewang/images/week04/a_ide.jpg" alt="16 pin connection with Arduino UNO" width="400" height="300">



## 📘 Arduino LCD Reference Manual
For Students Exploring Display Interfaces Using Arduino UNO
Prepared by: [Your Name, STEM Teacher]

### 📌 What You Will Learn:
- Introduction to LCDs and Arduino
- Components & Tools Needed
- Understanding LCD Types: 16-pin vs I2C
- Step-by-Step Wiring Guide
- Arduino Code Examples
- Troubleshooting Tips

### Keywords to Explore Further

#### 🧠 1. Basic Terminologies
Before starting, here are a few key terms you’ll encounter:

| **Term**        | **Meaning**                                      | **Search Keyword**              |
|-----------------|--------------------------------------------------|---------------------------------|
| LCD             | Liquid Crystal Display                           | “LCD 16x2 Arduino”              |
| Pin             | A connection point on a component                | “Arduino Pinout”                |
| I2C             | A communication protocol used for sensors/modules| “I2C Communication Arduino”     |
| Potentiometer   | A variable resistor used to adjust brightness    | “Arduino LCD Contrast”          |
| Breadboard      | A board for prototyping electronics              | “Breadboard Arduino Projects”   |
| Sketch          | A program written in Arduino IDE                 | “Arduino Sketch Examples”       |


#### 🔧 2. Components Required
For both types of LCDs, you will need:

- Arduino UNO

- USB cable (Type B) for Arduino
- LCD 16x2 module (16-pin)

- I2C LCD module (4-pin)

- Breadboard and jumper wires

- 10kΩ potentiometer (for 16-pin LCD)

- Resistors (if needed for backlight)

- Arduino IDE installed on your computer

#### 🖥️ 3. Setting Up the Arduino IDE
Before coding:

##### With Hardware

Download and install the Arduino IDE from https://www.arduino.cc/en/software.

Connect the Arduino UNO to your laptop using a USB cable.

Open Arduino IDE and select:

Board: Arduino UNO.

<img src="https://fabacademy.org/2025/labs/dgi/students/tsheyang-tshewang/images/week08/ide.jpg" alt="16 pin connection with Arduino UNO" width="400" height="300">

Port: COM port assigned to the Arduino

<img src="https://fabacademy.org/2025/labs/dgi/students/tsheyang-tshewang/images/week08/ide_port.jpg" alt="16 pin connection with Arduino UNO" width="400" height="300">

*you can use the Wok-wi or tinkercad simulation*

🔌 4. Interfacing 16x2 LCD (16-pin)
🔩 Pin Mapping
| **LCD Pin** | **Label** | **Connects To**                          |
|-------------|-----------|-------------------------------------------|
| 1           | GND       | GND on Arduino                            |
| 2           | VCC       | 5V on Arduino                             |
| 3           | VO        | Middle pin of potentiometer               |
| 4           | RS        | Digital Pin 12                            |
| 5           | RW        | GND                                       |
| 6           | E         | Digital Pin 11                            |
| 7–10        | D0–D3     | Not connected (used in 8-bit mode only)   |
| 11–14       | D4–D7     | Digital Pins 5, 4, 3, 2                    |
| 15          | LED+      | 220Ω resistor to 5V                       |
| 16          | LED-      | GND                                       |

<img src="Images/robotics_images/lcd/connection.png" alt="16 pin connection with Arduino UNO" width="400" height="300">


🧑‍💻 Sample Code for 16-Pin LCD
```cpp
#include <LiquidCrystal.h>

// RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  lcd.begin(16, 2); // 16 columns and 2 rows
  lcd.print("Hello, World!");
}

void loop() {
  // nothing here
}
```
<img src="https://gitlab.com/anithghalley/robotics_for_students/-/raw/main/Images/robotics_images/lcd/lcd_simulate.png?ref_type=heads" alt="16 pin connection with Arduino UNO" width="400" height="300">

#### Display On and Off

This example sketch shows how to use the display() and noDisplay() methods to turn on and off the display.

```cpp
#include <LiquidCrystal.h>

// RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  lcd.begin(16, 2); // 16 columns and 2 rows
  lcd.print("Hello, World!");
}

void loop() {
  lcd.noDisplay();
  delay(500);
  // Turn on the display:
  lcd.display();
  delay(500);
}
```
#### Display with Timmer.

```cpp
#include <LiquidCrystal.h>

// RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  lcd.begin(16, 2); // 16 columns and 2 rows
  lcd.print("Hello, World!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(millis() / 1000);
}
```

<img src="https://gitlab.com/anithghalley/robotics_for_students/-/raw/main/Images/robotics_images/lcd/lcd_with_timer.png?ref_type=heads" alt="16 pin connection with Arduino UNO" width="400" height="300">

🔌 5. Interfacing 16x2 LCD Using I2C (4-pin)
The I2C module is soldered to the back of the LCD, reducing pin usage.

🔩 Pin Mapping
I2C Pin	Label	Connects To
GND	Ground	GND on Arduino
VCC	Power	5V on Arduino
SDA	Serial Data	A4 on Arduino
SCL	Serial Clock	A5 on Arduino

<img src="https://lastminuteengineers.com/wp-content/uploads/arduino/I2C-LCD-Display-Pinout.png" alt="16 pin connection with Arduino UNO" width="400" height="300">


⚙️ Install I2C Library
Open Arduino IDE → Sketch → Include Library → Manage Libraries…

Search and install: LiquidCrystal I2C (by Frank de Brabander or similar)

🧑‍💻 Sample Code for I2C LCD

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// LCD address is usually 0x27 or 0x3F
LiquidCrystal_I2C lcd(0x27, 16, 2);  

void setup() {
  lcd.init();            
  lcd.backlight();       
  lcd.print("Hello I2C LCD");
}

void loop() {
  // nothing here
}
```

<img src="https://gitlab.com/anithghalley/robotics_for_students/-/raw/main/Images/robotics_images/lcd/i2c_lcd.png?ref_type=heads" alt="I2C LCD showing “Hello I2C LCD" width="400" height="300">



⚠️ 6. Common Troubleshooting Tips
| **Issue**             | **Solution**                                  |
|------------------------|-----------------------------------------------|
| LCD shows no text      | Adjust potentiometer (for 16-pin)             |
| I2C LCD not working    | Check address using I2C Scanner sketch        |
| Garbage text           | Ensure correct wiring & baud rate             |
| No power               | Recheck GND and VCC connections               |


🧭 7. Keywords for Further Learning
You can learn more by searching these topics:

"Arduino LCD vs I2C"

"Arduino LCD Potentiometer Contrast"

"Arduino I2C Scanner"

"Arduino LCD scrolling text"

"Custom characters on LCD Arduino"

✅ Final Notes
Using the 4-pin I2C LCD simplifies wiring but requires the I2C library and address check.

The 16-pin LCD gives you hands-on experience with control and data pins.

Always power off your Arduino before re-wiring.

Ask your teacher if you want to try custom animations, sensor data display, or interactive menus using LCDs.

Reference : [Tsheltrim Lhamo](https://fabacademy.org/2025/labs/dgi/students/tsheltrim-lhamo/assignments/week_04.html)
, [Tsheyang Palki Tshewang](https://fabacademy.org/2025/labs/dgi/students/tsheyang-tshewang/assignments/week05/).
