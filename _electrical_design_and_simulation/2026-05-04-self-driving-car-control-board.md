---
title: 'Eagle PCB Design for an Autonomous Crane Car Competition Robot'
date: 2026-05-04 00:00:02
featured_image: /images/electrical_design_and_simulation/selfdriving_car_modeling/modeling_car_2.jpg
excerpt: Design and fabrication of a custom ESP32-based control PCB in Autodesk Eagle for a competition robot — an autonomous RC car carrying a motorised crane arm capable of detecting and picking up objects.
---

![Crane Car Competition Robot](/images/electrical_design_and_simulation/selfdriving_car_modeling/modeling_car_2.jpg)

## Overview

This project was built for a **robotics competition** requiring an autonomous vehicle to navigate to objects and retrieve them using a motorised crane. The car had to operate fully autonomously — driving, positioning, extending the crane arm, and picking up targets without human input.

The custom control electronics were designed from scratch in **Autodesk EAGLE**, etched in-house, assembled, and integrated onto the RC car chassis.

---

## The Challenge

The competition task demanded simultaneous control of multiple independent systems:

- **Autonomous navigation** — driving to a target position without manual control
- **Crane actuation** — extending and retracting a boom arm precisely enough to pick up an object
- **Object interaction** — triggering a gripper or hook mechanism at the right moment

All of this had to run from a single embedded controller, coordinating motor drive outputs, sensor reads, and servo commands in real time.

---

## System Architecture

| Subsystem | Implementation |
|-----------|---------------|
| **Main controller** | ESP32 (dual-core, 240 MHz, Wi-Fi + Bluetooth) |
| **Drive motors** | Two DC motors via dual H-bridge motor driver ICs |
| **Crane actuation** | Servo motor(s) controlling arm extension and gripper |
| **Power supply** | LiPo battery pack with regulated 3.3 V / 5 V rails |
| **Comms** | Wi-Fi for telemetry and remote monitoring during testing |

---

## PCB Design in Eagle

![Custom Control PCB with ESP32](/images/electrical_design_and_simulation/selfdriving_car_modeling/modeling_car.jpg)

The control board was laid out in **Autodesk EAGLE** and fabricated in-house on single-sided copper-clad FR4. EAGLE's schematic-to-layout workflow was used throughout: the schematic was fully captured with net connections before switching to the PCB editor, ensuring the layout was electrically validated against the design before committing to fabrication.

### ESP32 Microcontroller

The **ESP32** sits at the centre of the design, providing:

- **PWM outputs** — independent channels driving each motor driver enable pin, controlling speed of both drive wheels and the crane lift motor
- **Direction GPIO** — logic-level signals into the motor driver direction inputs
- **Servo PWM** — 50 Hz PWM signal to the crane servo(s) for position control
- **Sensor inputs** — ADC and digital GPIO for distance sensors or limit switches on the crane
- **Wi-Fi** — used during development for live telemetry and remote parameter tuning without reflashing firmware

### Motor Driver ICs

Two **DIP-package dual H-bridge motor driver ICs** handle the four motor outputs:

- One IC drives the **left and right differential drive motors**, enabling forward, reverse, and steering by varying relative wheel speeds
- The second IC handles the **crane lift motor**, controlling extend and retract of the boom arm

DIP packages were deliberately chosen for the competition build — they are hand-solderable, replaceable in the field, and survive the rough handling of a competition environment better than fine-pitch SMD parts.

### Passive Components

The through-hole resistor array visible on the board provides:

- **Base resistors** for any BJT-buffered control signals
- **Pull-up/pull-down resistors** on ESP32 GPIO pins to define safe default states (e.g. motors off) at power-up before firmware initialises the outputs
- **Current-limiting resistors** for status LEDs indicating motor direction and enable state

### Wiring Harness

The colour-coded wire harness connects the board to the full vehicle:

| Colour | Function |
|--------|----------|
| Red / Black | LiPo power and ground |
| Yellow / Orange | Drive motor A and B |
| Purple | Crane lift motor |
| Brown | Servo signal |
| Red / Yellow striped | Sensor power and signal |

---

## PCB Fabrication

![PCB Reverse — Trace Layout and Through-Hole Soldering](/images/electrical_design_and_simulation/selfdriving_car_modeling/car_modeling_3.jpeg)

The board was fabricated using the **toner-transfer chemical etching** process:

1. Layout exported from EAGLE as a mirrored top-copper PDF
2. Toner heat-transferred onto cleaned copper-clad FR4 board
3. Board etched in **ferric chloride** solution to remove unmasked copper
4. Toner stripped with acetone, leaving clean copper traces
5. Holes drilled for all through-hole leads and board mounting screws
6. Components hand-soldered, starting with ICs then passives then connectors

The reverse side of the board shows the characteristic hand-etched single-layer trace layout — the two large DIP IC footprints dominate the left half of the board, with the ESP32 header spanning the right and the passive component field filling the centre.

---

## Autonomous Control Logic

The competition run sequence implemented in firmware:

1. **Initialise** — zero all motor outputs, run self-check on sensor readings
2. **Navigate** — drive toward target using distance sensor data to correct heading
3. **Position** — slow to a stop at pick-up distance; use fine sensor data for final alignment
4. **Deploy crane** — PWM ramp-up to extend the boom arm at a controlled speed
5. **Grip** — trigger the gripper servo at the target extension position
6. **Retract** — retract boom with object secured
7. **Return** — navigate back to the drop zone and release

Wi-Fi telemetry logged each stage transition in real time, allowing post-run analysis of where navigation errors occurred.

---

## Outcome

The assembled robot successfully demonstrated autonomous crane operation in competition conditions. The custom PCB provided reliable motor drive and servo control throughout, with the ESP32's dual-core architecture allowing navigation logic to run on one core while motor PWM outputs were managed on the other — avoiding the timing conflicts that arise when both run in the same execution loop.
