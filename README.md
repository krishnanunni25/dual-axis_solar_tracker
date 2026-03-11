# Dual-Axis Solar Tracker using ESP32

An automated solar tracking system that continuously aligns a solar panel toward the direction of maximum sunlight using an **ESP32 microcontroller**, **four LDR sensors**, and **two servo motors**.

The system detects differences in light intensity from multiple directions and adjusts the orientation of the solar panel along **two axes (horizontal and vertical)** to maximize solar energy capture.

---

## Demo Video

Video Link: https://youtube.com/shorts/ap8c8DNn0oo?feature=share

---

## Overview

Solar panels generate maximum power when sunlight strikes them **perpendicularly**. In fixed installations, the panel remains at a constant angle, which reduces efficiency as the sun moves across the sky.

This project implements a **dual-axis solar tracker** that automatically rotates the panel in both:

* **Azimuth (East-West movement)**
* **Altitude (Up-Down movement)**

Using four light sensors placed around the panel, the system determines the direction of stronger illumination and adjusts the panel orientation using servo motors.

---

## Features

* Dual-axis solar tracking
* Real-time light sensing using LDR sensors
* Automatic servo motor control
* Adjustable tracking thresholds to avoid jitter
* LCD display for voltage monitoring
* Toggle button to enable or disable automatic tracking
* Serial monitoring for debugging and data observation

---

## System Architecture

The system consists of the following main modules:

1. **Sensor Module**

   * Four LDR sensors arranged in a quadrant configuration
   * Detects directional light imbalance

2. **Control Unit**

   * ESP32 microcontroller processes sensor readings
   * Calculates horizontal and vertical differences

3. **Actuation System**

   * Two servo motors rotate the panel
   * One servo controls horizontal movement
   * One servo controls vertical movement

4. **Monitoring System**

   * LCD display shows solar panel voltage
   * Serial monitor outputs sensor and system data

---

## Hardware Components

* ESP32 microcontroller
* 4 × LDR (Light Dependent Resistors)
* 4 × 10kΩ resistors
* 2 × Servo motors
* LCD display
* Push button
* Indicator LED
* Small solar panel
* Breadboard and jumper wires

---

## Working Principle

Four LDR sensors are placed at the **top, bottom, left, and right** of the solar panel.

The ESP32 continuously reads the analog values from each sensor and calculates two differences:

* **Horizontal difference** → between left and right sensors
* **Vertical difference** → between top and bottom sensors

If the difference exceeds a predefined threshold:

* The corresponding servo motor rotates slightly toward the **brighter direction**.
* The panel gradually aligns with the strongest light source.

Servo rotation is constrained between **30° and 150°** to prevent mechanical over-rotation.

---

## Control Logic

1. Read analog values from all LDR sensors
2. Calculate horizontal and vertical light differences
3. Compare the difference with predefined cutoff thresholds
4. Adjust servo angles in small steps
5. Repeat continuously to maintain alignment

A push button allows the user to **toggle automatic tracking mode**.

When tracking is active:

* The LED indicator turns ON
* Servos automatically adjust the panel

---

## Power Monitoring

The system also measures the solar panel voltage using an analog input on the ESP32.

The measured voltage is:

* Displayed on the LCD screen
* Printed to the serial monitor for observation

This enables basic monitoring of the panel’s electrical output.

---

## Code Structure

The firmware performs the following tasks:

* Initialization of sensors, servos, LCD, and input pins
* Continuous sensor sampling
* Light intensity comparison
* Servo angle adjustment
* Voltage measurement
* LCD display updates
* Serial debugging output

The main program loop performs sensor reading, decision making, and actuator control in real time.

---

## How to Run the Project

1. Connect the hardware according to the circuit diagram.
2. Install the required Arduino libraries:

   * `ESP32Servo`
   * `LiquidCrystal`
3. Open the firmware file in **Arduino IDE**.
4. Select the appropriate **ESP32 board**.
5. Upload the code to the ESP32.
6. Power the system and enable tracking using the control button.

---

## Applications

* Solar panel efficiency optimization
* Renewable energy education and demonstrations
* Embedded systems learning projects
* Low-cost solar tracking prototypes

---

## Possible Improvements

Future improvements may include:

* Weather-proof mechanical structure
* Higher torque motors for larger panels
* Predictive solar tracking using astronomical algorithms
* GPS and real-time clock integration
* Data logging and IoT monitoring

---

## License

This project is released under the **MIT License**.
Feel free to use, modify, and distribute the code for educational and research purposes.
