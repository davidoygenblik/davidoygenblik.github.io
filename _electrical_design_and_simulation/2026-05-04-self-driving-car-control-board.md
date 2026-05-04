---
title: 'Custom Control PCB for an Autonomous RC Car Platform'
date: 2026-05-04 00:00:02
featured_image: /images/electrical_design_and_simulation/selfdriving_car_modeling/modeling_car_2.jpg
excerpt: Design, fabrication, and integration of a custom ESP32-based control PCB for a self-driving RC car, including motor driver interfacing, sensor wiring, and a boom-mounted camera for vision-based autonomous navigation.
---

![Autonomous RC Car Platform](/images/electrical_design_and_simulation/selfdriving_car_modeling/modeling_car_2.jpg)

## Overview

This project involved building a custom **control PCB** for an autonomous RC car platform — a small-scale testbed for experimenting with self-driving algorithms. The board integrates an **ESP32 microcontroller**, motor driver ICs, and sensor interfaces, all mounted directly onto the car chassis as a single compact board.

The PCB was designed, etched in-house, assembled, and wired up to the car's motors, sensors, and a boom-mounted camera to create a full autonomous vehicle platform.

---

## System Architecture

The car is built around three main electrical subsystems:

| Subsystem | Implementation |
|-----------|---------------|
| **Main controller** | ESP32 development module (Wi-Fi + Bluetooth capable) |
| **Motor drive** | Dual DIP-package motor driver ICs |
| **Perception** | Camera on adjustable boom arm |
| **Power** | LiPo battery pack with distribution to MCU and drivers |

---

## Custom PCB

![Control PCB — Top View with ESP32 Mounted](/images/electrical_design_and_simulation/selfdriving_car_modeling/modeling_car.jpg)

### ESP32 Microcontroller

The **ESP32** was chosen as the main controller for its combination of processing capability, onboard Wi-Fi/Bluetooth, and the breadth of available peripherals (PWM, I²C, SPI, ADC). It handles:

- Generating **PWM signals** for motor speed control
- Reading encoder or sensor inputs for closed-loop feedback
- Communicating with the camera module over a serial interface
- Enabling over-the-air (OTA) firmware updates and wireless telemetry via Wi-Fi

The ESP32 dev module mounts directly onto the custom PCB via its 38-pin header footprint, keeping it replaceable without reflowing the board.

### Motor Driver Stage

Two **DIP-package motor driver ICs** (visible in the centre of the board) provide H-bridge switching for independent control of the left and right drive motors. Each channel supports:

- Forward and reverse direction via logic-level direction inputs from the ESP32
- Speed control via PWM enable inputs
- Built-in overcurrent protection and thermal shutdown

Through-hole DIP packages were selected to allow easy replacement during development iterations.

### Passive Components and Signal Conditioning

The through-hole resistors populating the board serve multiple roles:
- **Pull-up/pull-down resistors** on digital inputs to define default states when ESP32 GPIO pins float
- **Current-limiting resistors** for indicator LEDs
- **Filter resistors** on motor feedback lines to reduce switching noise reaching the ADC inputs

### Wiring Harness

A multi-wire harness (coloured wires — power in black/red, motor drive in yellow/orange, sensor lines in purple/brown) connects the PCB to:
- **Drive motors** — rear wheels
- **Steering servo** — front wheel direction control
- **Sensor peripherals** — distance sensors or encoder feedback
- **LiPo supply** — battery to power rail input

---

## PCB Fabrication

![PCB Reverse — Through-Hole Soldering and Trace Layout](/images/electrical_design_and_simulation/selfdriving_car_modeling/car_modeling_3.jpeg)

The PCB was fabricated using the **toner-transfer chemical etching** process on single-sided copper-clad FR4:

1. Layout artwork generated and printed mirrored
2. Toner transferred to copper-clad board under heat and pressure
3. Board etched in **ferric chloride** to remove unprotected copper
4. Holes drilled for all through-hole component leads and mounting screws
5. Components hand-soldered

The reverse side of the board shows the characteristic appearance of a hand-etched single-sided PCB — clean copper traces with hand-drilled through-holes and point-to-point solder joints for component leads.

---

## Camera and Perception Mount

The car uses a **boom-arm mounted camera** — visible extending above the car chassis in the platform photo. The elevated mounting position gives the camera a forward-looking, wide-field-of-view angle, similar to a forward-facing driving camera, without ground-level obstruction from the chassis or wheels.

The camera feed is processed either on-board (via the ESP32-CAM variant's onboard image processor) or streamed wirelessly to an external machine running the navigation algorithm, depending on the compute requirements of the autonomy stack being tested.

---

## Autonomous Navigation

The platform is designed as a flexible testbed. The combination of:
- **ESP32 Wi-Fi** for remote control override and telemetry
- **Camera vision** for lane/obstacle detection
- **PWM motor control** for precise speed and steering commands

...allows the car to be used for experimenting with algorithms ranging from simple line-following using colour thresholding through to more involved computer vision pipelines running on a connected host.

---

## Outcome

The assembled platform successfully operated as a self-driving testbed, with the custom PCB reliably interfacing the ESP32 to the drive system. The in-house fabrication process allowed rapid iteration on the board layout as the system requirements evolved during development.
