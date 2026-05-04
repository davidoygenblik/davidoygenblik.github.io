---
title: 'MOSFET-Based Electromagnet Control Circuit — Design and Fabrication'
date: 2026-05-04 00:00:01
featured_image: /images/electrical_design_and_simulation/electromagnet_control/electro1.jpeg
excerpt: Design of a MOSFET-switched electromagnet control circuit in Altium Designer, from schematic capture and PCB layout through to in-house etching and physical testing of the fabricated boards.
---

## Overview

This project covers the end-to-end design and fabrication of a **MOSFET-based electromagnet control circuit** — from schematic capture in **Altium Designer** through to physically etched and assembled PCBs tested in the lab.

The circuit drives an inductive electromagnet load using a switched MOSFET, with a BJT-based gate driver stage to ensure fast, reliable switching.

---

## Circuit Design

### Topology

The control circuit uses a two-stage switching approach:

1. **BJT gate driver (2N3904 NPN transistor)** — takes a logic-level input signal and drives the MOSFET gate with sufficient current to switch it quickly, avoiding prolonged time in the linear region and the associated power dissipation
2. **P-channel power MOSFET (FED140P)** — the main switching element controlling current through the electromagnet coil

Using a P-channel MOSFET on the high side simplifies the gate drive requirements: when the gate is pulled low (relative to source) by the BJT, the MOSFET turns on and supplies current to the coil.

### Key Components

| Component | Part | Function |
|-----------|------|----------|
| Q1 | 2N3904 NPN BJT | Gate drive / level shifter |
| Q2 | FED140P P-channel MOSFET | High-side electromagnet switch |
| R1–R2 | Resistor divider | Gate resistors — limit gate current, control switching speed |
| R3–R5 | Bias resistors (1 kΩ, 2 kΩ, 4.7 kΩ) | BJT base bias network |
| JP1–JP6 | 2-pin headers | Input signal, power supply, and coil load connections |

### Flyback Protection

An inductive load like an electromagnet coil stores energy in its magnetic field. When the MOSFET switches off, this energy must be dissipated — without a flyback diode, the resulting voltage spike can exceed the MOSFET's drain-source breakdown voltage and destroy the device. A **flyback (freewheeling) diode** is placed in anti-parallel across the coil terminals to provide a safe recirculation path for the inductive kick.

---

## PCB Layout in Altium

![Altium PCB Layout — Top and Bottom Copper Layers](/images/electrical_design_and_simulation/electromagnet_control/electro1.jpeg)

The PCB layout was completed in Altium Designer. The two-layer view shows:

- **Blue (top copper)** — signal routing, component pads, and the gate drive network
- **Red (bottom copper)** — power traces carrying the coil supply current, routed wider to handle the higher current without excessive resistive loss

### Layout Decisions

- **Component placement** — the 2N3904 BJT is placed immediately adjacent to the MOSFET gate pad to minimise the gate drive loop area, reducing switching noise
- **Trace widths** — power traces to the coil are sized using the IPC-2221 standard for the expected current level; signal traces use the minimum manufacturable width
- **Header placement** — all external connections (input signal, supply, coil) are grouped at the board edges for clean wiring in the final assembly
- **Silkscreen labelling** — component designators and connector pin 1 markers added to aid assembly

---

## Fabrication — In-House PCB Etching

![Etched PCBs Ready for Assembly](/images/electrical_design_and_simulation/electromagnet_control/Electro2.JPG)

Rather than sending to a PCB manufacturer, the boards were fabricated in-house using the **toner transfer / chemical etching** process on single-sided **FR4 copper-clad laminate**:

1. PCB artwork printed as a mirror image onto transfer paper
2. Toner heat-transferred onto the copper-clad board
3. Board submerged in **ferric chloride (FeCl₃)** etchant to remove unprotected copper
4. Toner residue cleaned with acetone, leaving the copper traces
5. Holes drilled for through-hole component leads and mounting points

Three board variants were etched across the session, visible in the photo — the different sizes correspond to layout iterations and separate sub-circuit sections tested independently before combining.

---

## Lab Testing and Electromagnet Integration

![Electromagnet Coil and Test Setup](/images/electrical_design_and_simulation/electromagnet_control/Electro3.png)

With the boards assembled, the electromagnet coil itself was wound and tested on the bench. The lab setup shows:

- The wound **electromagnet coil** clamped in a test jig
- A **bench power supply** (background) providing the coil drive voltage
- The control PCB receiving a logic-level PWM input, with coil current measured via a series shunt

Switching behaviour was verified with an oscilloscope across the MOSFET drain, confirming:
- Clean turn-on and turn-off transitions
- Flyback spike clamped within the MOSFET's safe operating area
- Stable operation across the target duty-cycle range

---

## Outcome

The control circuit successfully switched the electromagnet coil with reliable on/off behaviour and no component failures across the test duration. The in-house etching process demonstrated a fast, low-cost route from Altium layout to physical board — particularly useful for iterating on the design before committing to a professionally manufactured PCB.
