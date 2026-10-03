# SMART_EXAM_HALL_MONITORING_SYSTEM
To develop an intelligent system that automatically monitors the examination hall by detecting unauthorized activities, monitoring environmental conditions, and sending real-time alerts to the invigilator.
🎓 Smart Exam Hall Monitoring & Management System

«A real-time embedded system for automated, secure, and efficient examination hall management using the NXP LPC2148 ARM7 microcontroller.»

📌 Project Overview

The Smart Exam Hall Monitoring & Management System is an Embedded C project designed to automate important examination-hall operations such as exam scheduling, countdown management, temperature monitoring, password-protected settings, pause/resume control, and exam-end alerts.

The system is developed using the NXP LPC2148 ARM7TDMI-S microcontroller and integrates multiple peripherals including RTC, LCD, keypad, 7-segment display, ADC, LM35 temperature sensor, LEDs, buzzer, and external interrupts.

The project demonstrates practical implementation of:

- Embedded C programming
- ARM7 microcontroller programming
- GPIO interfacing
- ADC
- RTC
- Timers
- External interrupts
- LCD interfacing
- Keypad interfacing
- 7-segment multiplexing
- Sensor interfacing
- Password-based access control

---

🎯 Objectives

- Automate examination timing and countdown.
- Display real-time date and time.
- Monitor examination-hall temperature.
- Provide password-protected system settings.
- Allow authorized users to configure exam parameters.
- Provide pause/resume functionality.
- Generate visual alerts as the exam approaches its end.
- Generate an audible alert when the examination ends.
- Reduce manual monitoring and timekeeping.

---

✨ Key Features

Feature| Description
⏱️ Exam Countdown| Automatically starts the countdown when the RTC reaches the configured exam start time.
🔐 Password Protection| A 4-digit PIN protects system settings.
📅 RTC| Displays and manages real-time date and time.
🌡️ Temperature Monitoring| LM35 temperature sensor is read using ADC.
⏸️ Pause / Resume| Exam countdown can be paused and resumed using an external interrupt.
🔢 7-Segment Display| Displays the remaining examination time.
🖥️ 20×4 LCD| Displays time, date, temperature, status, and duration.
💡 LED Alerts| LEDs provide warnings as the examination approaches its end.
🔊 Buzzer| Sounds when the examination duration reaches zero.
⌨️ 4×4 Keypad| Used for configuration and user input.

---

🧠 System Working

                 ┌──────────────────────┐
                 │      LPC2148         │
                 │      ARM7 MCU        │
                 └──────────┬───────────┘
                            │
       ┌────────────────────┼────────────────────┐
       │                    │                    │
       ▼                    ▼                    ▼
     RTC                  Keypad              LM35
       │                    │                    │
       │                    │                    ▼
       │                    │                   ADC
       │                    │                    │
       ▼                    ▼                    ▼
   Time/Date          User Settings        Temperature
       │
       ▼
   Exam Start
       │
       ▼
  Countdown Timer
       │
       ├───────────────┐
       │               │
       ▼               ▼
   7-Segment         LED Alerts
       │
       ▼
  Duration = 0
       │
       ▼
     Buzzer

---

🔄 Exam Operation

Power ON
   ↓
Initialize peripherals
   ↓
Display system information
   ↓
Enter password-protected settings
   ↓
Configure RTC / Exam Start Time / Duration
   ↓
Wait for configured exam start time
   ↓
Exam starts
   ↓
Countdown begins
   ↓
Monitor temperature
   ↓
Display remaining time
   ↓
LED warning according to remaining time
   ↓
Optional Pause / Resume
   ↓
Countdown reaches 0
   ↓
Buzzer ON
   ↓
System ready for next examination

---

🚦 LED Alert System

The LEDs provide visual warnings according to the remaining examination time.

Remaining Time| Alert
> 15 minutes| All LEDs OFF
≤ 15 minutes| LED3 ON
≤ 10 minutes| LED2 ON, LED3 OFF
≤ 5 minutes| LED1 ON, LED2 OFF
0 minutes| Buzzer ON for 3 seconds

---

🔐 Password System

The system uses a 4-digit password to protect configuration settings.

Default Password

1234

After successful authentication, the authorized user can configure:

- RTC time
- RTC date
- Exam start time
- Exam duration
- Password

The password input is masked on the LCD.

---

🌡️ Temperature Monitoring

The LM35 temperature sensor is connected to the LPC2148 ADC.

Working

LM35
 ↓
Analog Voltage
 ↓
ADC Channel
 ↓
10-bit ADC Conversion
 ↓
Voltage Calculation
 ↓
Temperature Calculation
 ↓
LCD Display

For a 3.3 V ADC reference:

ADC Step = 3.3 / 1024

The LM35 provides approximately:

10 mV / °C

The calculated temperature is displayed on the LCD.

---

⏸️ Pause / Resume Function

The system uses an external interrupt for pause/resume functionality.

EINT2
  ↓
Pause Exam
  ↓
Countdown Stops
  ↓
EINT2 Again
  ↓
Resume Exam

The paused duration is excluded from the examination's elapsed-time calculation.

---

⚡ Interrupts Used

Interrupt| Function
EINT0| Opens the password-protected settings menu
EINT2| Pauses / resumes the examination
Timer0 ISR| Generates periodic timing and multiplexes the 7-segment display

---

🔌 Hardware Components

No.| Component| Specification| Purpose
1| Microcontroller| NXP LPC2148 ARM7TDMI-S| Main controller
2| LCD| 20×4 Character LCD| Display
3| Keypad| 4×4 Matrix Keypad| User input
4| 7-Segment| 2-digit Common Anode| Countdown
5| Temperature Sensor| LM35| Temperature measurement
6| RTC| LPC2148 Internal RTC| Time/date
7| LEDs| 3 LEDs| Warning indication
8| Buzzer| Active Buzzer| Exam-end alert
9| Push Buttons| EINT0 / EINT2| Settings and pause/resume

---

📍 Pin Configuration

Port 0

LPC2148 Pin| Function
P0.5| Buzzer
P0.8 – P0.15| LCD Data
P0.16| LCD RS
P0.17| LCD Enable
P0.19| 7-Segment Digit Select 1
P0.20| 7-Segment Digit Select 2
P0.27| LED1
P0.28| LED2
P0.29| LED3

Port 1

LPC2148 Pin| Function
P1.16 – P1.19| Keypad Rows
P1.20 – P1.23| Keypad Columns
P1.24 – P1.31| 7-Segment Segment Data

Interrupt / ADC

Pin / Peripheral| Function
EINT0| Settings
EINT2| Pause / Resume
ADC Channel 3| LM35 Temperature Input

---

📁 Project Structure

SMART_EXAM_HALL_MONITORING_SYSTEM/
│
├── Project/
│
│   ├── inc/
│   │   ├── types.h
│   │   ├── defines.h
│   │   ├── rtc_defines.h
│   │   ├── lcd_defines.h
│   │   ├── kpm_defines.h
│   │   ├── seg_defines.h
│   │   ├── adc_defines.h
│   │   ├── io_defines.h
│   │   ├── all_macros.h
│   │   ├── lcd.h
│   │   ├── kpm.h
│   │   ├── delay.h
│   │   ├── seg.h
│   │   ├── adc.h
│   │   ├── lm35.h
│   │   ├── rtc.h
│   │   ├── exam.h
│   │   └── password.h
│   │
│   ├── src/
│   │   ├── lcd.c
│   │   ├── kpm.c
│   │   ├── delay_def.c
│   │   ├── seg.c
│   │   ├── adc.c
│   │   ├── lm35.c
│   │   ├── rtc.c
│   │   ├── password.c
│   │   └── exam.c
│   │
│   ├── Makefile
│   └── *.uvproj
│
└── README.md

---

🛠️ Development Environment

Tool| Details
Programming Language| Embedded C
Microcontroller| NXP LPC2148
Architecture| ARM7TDMI-S
CPU Frequency| 60 MHz
IDE| Keil µVision
Compiler| Keil ARM C Compiler
Flashing Tool| Flash Magic
Debugging| JTAG / Keil Simulator
Simulation| Proteus

---

🚀 Getting Started

1. Clone the Repository

git clone https://github.com/omkarsabale27/SMART_EXAM_HALL_MONITORING_SYSTEM.git

cd SMART_EXAM_HALL_MONITORING_SYSTEM

2. Open the Project

Open the project using:

Keil µVision

Open the ".uvproj" project file.

3. Configure Include Path

Add:

inc/

to the project's C/C++ include paths.

4. Add Source Files

Make sure all source files from:

src/

are included in the Keil project.

5. Select Target

Select:

NXP LPC2148

as the target microcontroller.

6. Build

Use:

Project → Build Target

or press:

F7

7. Flash the Microcontroller

Use Flash Magic through UART ISP or a suitable JTAG programmer to program the LPC2148.

---

🧩 Technologies & Concepts Used

Embedded C

- Functions
- Structures
- Pointers
- Header files
- Modular programming
- Interrupt Service Routines
- Bit manipulation
- Register-level programming

Microcontroller Peripherals

- GPIO
- ADC
- RTC
- Timer
- External Interrupts
- LCD
- Keypad
- 7-Segment Display

Embedded Concepts

- Interrupt handling
- Polling
- Multiplexing
- Sensor interfacing
- Real-time clock management
- State-based exam control
- Password authentication
- Time calculation
- Modular driver development

---

💼 Skills Demonstrated

This project demonstrates practical experience in:

Embedded C
      │
      ├── ARM7 / LPC2148
      ├── GPIO
      ├── ADC
      ├── RTC
      ├── Timers
      ├── Interrupts
      ├── LCD
      ├── Keypad
      ├── 7-Segment
      ├── LM35
      ├── Buzzer / LED
      └── Modular Driver Development

---

🎤 Interview Project Explanation

Short Version

«"I developed a Smart Exam Hall Monitoring and Management System using the LPC2148 ARM7 microcontroller and Embedded C. The system automatically manages exam timing using the internal RTC and displays the remaining time on a multiplexed 7-segment display. I interfaced a 4×4 keypad and 20×4 LCD for user interaction and configuration. An LM35 temperature sensor is connected through the ADC to monitor room temperature. I also implemented external interrupts for password-protected settings and pause/resume functionality, while LEDs provide time-based warnings and a buzzer indicates the end of the examination."»

---

📌 Future Improvements

Possible extensions include:

- RFID-based student attendance
- Fingerprint authentication
- ESP32/ESP8266 IoT connectivity
- Cloud-based exam monitoring
- Mobile notifications
- Multiple exam-hall monitoring
- Automatic attendance system
- Camera-based monitoring
- Web dashboard
- Data logging using EEPROM/SD card

---

👨‍💻 Author
Tanuja Chavan

Embedded Systems & Firmware Engineer | E&TC Graduate

GitHub



---

⭐ Project Highlights

Microcontroller : LPC2148 ARM7
Language        : Embedded C
Display         : 20×4 LCD + 2-Digit 7-Segment
Sensor          : LM35
Input           : 4×4 Keypad
Interrupts      : EINT0 + EINT2
Timer           : Timer0
Communication  : GPIO / Peripheral Interfacing
IDE             : Keil µVision
Simulation      : Proteus


