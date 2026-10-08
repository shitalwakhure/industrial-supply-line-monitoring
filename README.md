# Industrial Supply Line – Adaptive Material Monitoring & POST

## Project Overview

An ATmega328P-based intelligent material monitoring and supply-line safety system designed for an industrial manufacturing environment.

The system performs a **Power-On Self-Test (POST)** during startup to verify the availability and basic functionality of the sensors, LCD, LED indicators, and DC motor/actuator interface before entering normal operation.

During operation, the system continuously monitors:

- Temperature and humidity using DHT11
- Proximity/material distance using an ultrasonic sensor
- Orientation/movement using a gyro sensor
- Gas leakage using a gas sensor

The sensor readings are combined to classify the system into:

- **NORMAL**
- **WARNING**
- **CRITICAL**

Based on the detected condition, the system provides a local response through the LCD, LED board, and DC motor/actuator.

---

# Objectives

The main objectives of the project are:

1. Implement reliable Power-On Self-Test (POST).
2. Detect sensor availability and abnormal readings.
3. Continuously monitor environmental and material/supply-line conditions.
4. Detect obstacles and possible supply-line blockage.
5. Detect tilt, movement, and topple conditions.
6. Detect gas leakage and abnormal temperature.
7. Classify conditions into NORMAL, WARNING, and CRITICAL.
8. Provide real-time information through an LCD.
9. Provide distinct LED indications for different system states.
10. Automatically activate or stop the DC motor/actuator when required.
11. Implement hardware/software safety shutdown.
12. Demonstrate low-level ATmega328P programming without standard libraries.
13. Analyze power consumption, power-saving modes, and battery runtime.

---

# Hardware Components

The system uses only the components provided for the project together with the Arduino Uno SMD / ATmega328P platform.

### Main Controller

- ATmega328P
- Arduino Uno SMD

### Sensors

- DHT11 temperature/humidity sensor
- Ultrasonic proximity sensor
- Gyro/orientation sensor
- Gas leakage sensor

### Output Devices

- LCD
- LED board
- DC motor/actuator

### Safety

- Hardware/software kill switch

> No Wi-Fi, Ethernet module, external server, or additional sensor is used.

---

# System Architecture

```text
                    +----------------------+
                    |      ATmega328P      |
                    |      Arduino Uno     |
                    +----------+-----------+
                               |
          +--------------------+--------------------+
          |                    |                    |
          v                    v                    v
      DHT11              Ultrasonic              Gyro
 Temp / Humidity        Distance/Obstacle     Tilt/Motion
          |                    |                    |
          +--------------------+--------------------+
                               |
                               v
                         Gas Sensor
                               |
                               v
                    +----------------------+
                    | Sensor Data Fusion   |
                    | & Decision Engine    |
                    +----------+-----------+
                               |
             +-----------------+----------------+
             |                 |                |
             v                 v                v
          NORMAL            WARNING          CRITICAL
             |                 |                |
             +-----------------+----------------+
                               |
              +----------------+----------------+
              |                |                |
              v                v                v
             LCD              LED         DC Motor/
          Display            Indicator       Actuator
