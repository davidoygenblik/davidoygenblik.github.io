---
title: 'EV6 Shutdown Circuit Design for a Formula Student AI Car'
date: 2026-05-04 00:00:00
featured_image: /images/electrical_design_and_simulation/Shutdown-circuit-car/FS-AI.png
excerpt: Design and fabrication of an EV6-compliant shutdown circuit PCB for a Formula Student AI driverless racing car, covering the full safety chain from accumulator isolation to autonomous system watchdog integration.
---

![EV6 Shutdown Circuit Schematic](/images/electrical_design_and_simulation/Shutdown-circuit-car/FS-AI.png)

## Overview

This project involved the design of an **EV6-compliant shutdown circuit** for a **Formula Student AI (FS-AI)** driverless electric racing car. The shutdown circuit is one of the most safety-critical systems in any Formula Student EV — its job is to ensure that the high-voltage accumulator is immediately and reliably isolated from the tractive system whenever any safety condition is violated.

The design was implemented in **Altium Designer**, moving from system-level schematic capture through to a fabricated, conformal-coated multi-layer PCB.

---

## The EV6 Shutdown Circuit — How It Works

The shutdown circuit is a **series chain of normally-open (NO) and normally-closed (NC) contacts** wired through the low-voltage supply to the AIR (Accumulator Isolation Relay) coil activation logic. If any element in the chain opens, the AIRs de-energise and disconnect the accumulator from the tractive system.

### Safety Chain Elements

The implemented chain follows the Formula Student Germany EV rules and includes the following nodes in series:

| Node | Function |
|------|----------|
| **LVMS** | Low Voltage Master Switch — manual isolation of the LV system |
| **Overcurrent Protection** | Fuse/breaker protecting the LV shutdown bus |
| **BSPD** | Brake System Plausibility Device — opens if brakes are applied hard while significant motor current flows (detects stuck throttle) |
| **IMD** | Insulation Monitoring Device — detects insulation faults between HV and chassis |
| **AMS** | Accumulator Management System — monitors cell voltages and temperatures; opens on any out-of-range condition |
| **Cockpit Button** | Driver-accessible emergency shutdown, latching |
| **Left / Right Buttons** | External shutdown buttons on both sides of the car (marshals) |
| **TSMS** | Tractive System Master Switch — external key-operated switch |
| **HVD Interlock** | High Voltage Disconnect interlock loop — opens if the HVD plug is removed |
| **BOTS** | Brake Over-Travel Switch — NC switch that opens if the brake pedal travels beyond its mechanical limit (brake failure) |
| **Inertia Switch** | Opens on significant impact, preventing post-crash HV exposure |

### Autonomous-Specific Additions (DV Only)

For the FS-AI driverless class, two additional nodes are inserted into the chain:

- **RES (Remote Emergency Stop)** — a wireless kill switch operated by trackside officials; the car must stop within seconds of activation
- **AS (Autonomous System watchdog)** — the mission controller must send a periodic heartbeat signal; if communication is lost or a fault is detected, this node opens the chain

Additionally, the driverless rules require an **EBS (Emergency Brake System)** relay coil in the circuit. When the shutdown chain opens, the EBS relay drops out and applies the brakes autonomously — critical since there is no driver to brake the car.

---

## PCB Design

![PCB — Microcontroller and Power Section](/images/electrical_design_and_simulation/Shutdown-circuit-car/Car1.png)

The PCB implements the **activation logic and monitoring** side of the shutdown system. Key design decisions:

### Power Architecture

The board operates from the car's LV battery and requires an isolated supply for sections that interface with the HV-adjacent signals (IMD, AMS outputs). A **RECOM switching DC-DC converter** (UMT-H package, visible in the top-right of the PCB) provides this isolated rail, keeping the logic-side ground separated from the chassis ground reference used by the HV system.

### Voltage Monitoring Test Points

Multiple solder-pad test points are exposed on the board for in-car diagnostics and pre-scrutineering checks:

- **SP6 — 24.8 V** (accumulator low-state voltage)
- **SP8 — 28.8 V** (accumulator nominal voltage)
- **SP11 — 39.6 V** (accumulator charged voltage, monitored on the HV-adjacent section)

These allow the team to probe the accumulator state through the LV system without exposing HV test equipment.

### Microcontroller and Logic

An on-board microcontroller (clocked at **8 MHz** via crystal oscillator) manages:

- Reading the status of each node in the shutdown chain
- Driving status LEDs (OK, temp, fault indicators visible on the board)
- Communicating fault codes over the car's CAN bus for datalogging

### Switching and Output Stage

![PCB — MOSFET Output Stage Detail](/images/electrical_design_and_simulation/Shutdown-circuit-car/Car2.jpeg)

The output stage (bottom section of the PCB) drives the AIR coil and EBS relay. Visible components include:

- **Q1** — power MOSFET controlling the AIR coil current path
- **U4 / U3 / U5** — gate driver and logic ICs
- **C1** — bulk decoupling capacitor on the coil supply rail
- **R1 (120 Ω)** — current-limiting resistor in the gate drive path
- **R2** — pull-down to ensure the MOSFET is off in a power-loss condition (fail-safe)

The board is labelled **"Coated"** in the MOSFET output region — conformal coating was applied here to protect against moisture and vibration-induced failures during racing conditions.

---

## Design Considerations

- **Fail-safe defaults** — all relays and MOSFETs are driven such that a loss of power or signal opens the shutdown chain rather than closing it
- **Latching vs. non-latching** — cockpit and external buttons are latching (require deliberate reset); transient faults (e.g. IMD glitch) can be reset via a dedicated reset input
- **Conformal coating** — applied to high-voltage-adjacent and output areas to meet automotive environmental requirements
- **DRC and ERC** — full Design Rule Check and Electrical Rules Check run in Altium prior to Gerber generation, with trace widths calculated for the maximum expected coil drive current

---

## Outcome

The completed board was fabricated as a multi-layer PCB, assembled, and integrated into the FS-AI car's electrical system. The shutdown chain was verified against the Formula Student rules checklist, with each node individually tested for correct open/close behaviour before the car was presented at scrutineering.
