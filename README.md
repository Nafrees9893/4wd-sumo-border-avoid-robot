# 4WD Sumo-Style Border-Avoid & Obstacle-Pushing Robot

This repository contains the Arduino code for my 4-wheel robot car built with:

- **Adafruit Motor Shield v1**
- **HC-SR04 ultrasonic sensor**
- **Two IR line sensors** (border detection)
- **Standard servo** for sensor scanning (optional)

The robot can:

- Freely roam inside a white arena with a black border
- Detect the border using two down-facing IR sensors and avoid falling out
- Detect obstacles in front using an ultrasonic sensor
- Switch to a **push mode** to push the obstacle toward the arena border

---

## Features

- ✅ 4WD drive with **rugged mechanical design**
- ✅ Border detection using **two IR line sensors** (left & right)
- ✅ Obstacle detection using **HC-SR04 ultrasonic sensor**
- ✅ Two modes using a simple state machine:
  - `MODE_ROAM` – free roaming inside the arena
  - `MODE_PUSH` – high-speed pushing when an obstacle is detected
- ✅ Randomized turn when both IR sensors detect the border (helps escape corners)

---

## Hardware Used

- **Microcontroller:** Arduino (with Adafruit Motor Shield v1)
- **Motor Driver:** Adafruit Motor Shield v1
- **Motors:** 4 × DC geared motors (4WD robot chassis)
- **Ultrasonic Sensor:** HC-SR04 (trigger/echo)
- **IR Line Sensors:** 2 × IR reflection sensors (front-left, front-right)
- **Servo:** Standard servo for sensor scanning (on pin 10)
- **Power:** Battery pack for motors + regulated 5V for logic

---

## Pin Mapping

### Ultrasonic (HC-SR04)

| Function | Arduino Pin |
|---------|-------------|
| TRIG    | A1          |
| ECHO    | A0          |

### IR Line Sensors (Digital)

| Sensor       | Arduino Pin | Description                     |
|--------------|-------------|---------------------------------|
| IR Front Left  | A4        | Down-facing, near left front wheel  |
| IR Front Right | A5        | Down-facing, near right front wheel |

> **Note:** In the code we assume:  
> - White area → LOW (0)  
> - Black line → HIGH (1)  
> If your sensors work the opposite way, you can invert in software.

### Motors (Adafruit Motor Shield v1)

| Motor # | Position     | Side |
|--------|--------------|------|
| M1     | Front Left   | Left |
| M2     | Back Left    | Left |
| M3     | Back Right   | Right|
| M4     | Front Right  | Right|

Left side = M1 + M2  
Right side = M3 + M4  

### Servo

| Device | Arduino Pin |
|--------|-------------|
| Servo  | 10          |

---

## Code Overview

Main files:

- `firmware/4wd_sumo_bot.ino` – main Arduino sketch

Libraries used:

```cpp
#include <NewPing.h>
#include <Servo.h>
#include <AFMotor.h>
