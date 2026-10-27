# Gesture-Controlled Robot Car

A dual-Arduino system for a gesture-controlled robotic vehicle. It uses an MPU6050 accelerometer for hand-tracking and nRF24L01 modules for wireless communication. Additionally, it uses a LM2596 Step-down power, staying at a steady 5V, in order to not burn out the Nano.

## Features

- **Differential Steering:** Mixes X and Y axis tilt to control individual motor direction for smooth steering.
- **Deadzone Filter:** Ignores minor movements (values < 20) to prevent jitter and unwanted drifting.
- **Signal Failsafe:** Receiver automatically kills motor power if no radio data is received for 500ms.

## Hardware Requirements
- 2x LM2596 Step-Down module
- 2x Arduino Boards (Nano V3)
- 2x nRF24L01 Radio Modules
- 1x MPU6050 Accelerometer/Gyroscope Module (Transmitter)
- 1x Motor Driver (e.g., L298N) (Receiver)
- DC Motors & Chassis

## Pin Configuration

### Transmitter (Glove)

| Component | Arduino Pin |
| :--- | :--- |
| nRF24 CE | `9` |
| nRF24 CSN | `10` |
| MPU6050 SDA | `SDA` / `A4` |
| MPU6050 SCL | `SCL` / `A5` |

### Receiver (Car)

| Component | Arduino Pin |
| :--- | :--- |
| nRF24 CE | `9` |
| nRF24 CSN | `10` |
| Driver IN1 (Left Motor) | `A2` |
| Driver IN2 (Left Motor) | `A3` |
| Driver IN3 (Right Motor) | `A4` |
| Driver IN4 (Right Motor) | `A5` |

## Radio Settings

- **Channel:** 115
- **Data Rate:** 1 MBPS
- **PA Level:** LOW
- **Pipe Address:** `00001`
- **Payload:** 4-byte Struct (two 16-bit integers for X and Y coordinates, mapped from -100 to +100).

## Installation & Usage

1. Wire the components according to the pin configuration tables.
2. Install the required libraries in the Arduino IDE:
   - `RF24` by TMRh20
   - `Wire` (built-in)
3. Upload the Transmitter code to the Arduino mounted on the glove.
4. Upload the Receiver code to the Arduino mounted on the car chassis.
5. Power both systems. Tilt the MPU6050 to drive the car.
