# Light Intensity-Based Alarm and Parking Detection System

## Project Overview
This repository contains the code, circuit design, and documentation for a light intensity-based alarm and parking detection system. Built using an Arduino UNO and Light Dependent Resistors (LDRs), this system measures environmental light levels dynamically and produces corresponding, stepped audio frequencies through active buzzers to simulate a smart parking detection mechanism.

**Author:** Muhammad Khaleed Bin Huda  
**Institution:** Department of Mechatronics Engineering, Khulna University of Engineering & Technology (KUET)  
**Course:** MTE 2106 (Sessional on Sensors and Instrumentation)  

---

## Objective
To design and evaluate a responsive light intensity-based alarm system. The presence or absence of a physical obstruction (simulating a vehicle) is determined by the shadow it casts over the sensors, triggering discrete acoustic feedback based on proximity.

## Theory & Working Principle
A Light Dependent Resistor (LDR) is a variable passive component whose resistance decreases significantly as incident light increases. In this project, the LDR is implemented within a voltage divider circuit to convert the physical change in resistance into a measurable analog voltage.

The output voltage read by the Arduino's analog pin is governed by the voltage divider equation:
$$V_{out} = V_{in} \times \frac{R_{fixed}}{R_{LDR} + R_{fixed}}$$

In total darkness, the LDR possesses a high resistance, resulting in a specific voltage drop. Under bright illumination, the resistance drops, altering the analog voltage. The Arduino's 10-bit ADC translates this fluctuating voltage into an integer value ranging from 0 to 1023, which triggers the programmed buzzer frequencies.

## Components Used
* Arduino UNO (1x)
* Light Dependent Resistor / Photoresistor (2x)
* Active Buzzer (2x)
* Resistor - 1kΩ (2x)
* Jumper Wires & Breadboard

## Circuit Logic
* **Sensor Input:** Two LDRs are connected to Arduino analog pins `A0` and `A1`, each paired with a 1kΩ pull-down resistor to form a precise voltage divider network.
* **Audio Output:** Two active buzzers are connected to PWM-capable digital pins `9` and `10` to generate square waves for audio tones.

## Results and System States
The system was calibrated to map ambient light into distinct acoustic states:
* **Dark (ADC < 50):** 0Hz (Off state) – Indicates a fully parked or obstructed state.
* **Dim (ADC 50 - 99):** 100Hz (Buzzer 1) and 1500Hz (Buzzer 2).
* **Medium Bright (ADC 100 - 299):** 500Hz (Buzzer 1) and 2000Hz (Buzzer 2).
* **Very Bright (ADC >= 300):** 800Hz (Buzzer 1) and 2500Hz (Buzzer 2) – Indicates a clear, unobstructed sensor.

## Limitations and Future Improvements
* **Current Limitations:** The bare LDRs are susceptible to environmental noise, stray shadows, and the 50Hz/60Hz frequency flicker inherent in AC-powered overhead lighting, which can cause erratic ADC readings.
* **Future Work:** Implementing software filtering (like a moving average filter) in the C++ code to debounce light fluctuations. Placing the LDRs inside a 3D-printed collimator tube would narrow their field of view to block ambient room noise. Future iterations may integrate Ultrasonic (HC-SR04) or IR sensors for robust nighttime detection.

## References
1. Arduino Official Documentation: `analogRead()` and `tone()` functions.
2. Sessional Lab Manual - MTE 2106: Sensors and Instrumentation.
