# PLC-Based Control System for a 4-Floor Elevator

![PLC](https://img.shields.io/badge/PLC-ABB%20AC500-E30613)
![Standard](https://img.shields.io/badge/IEC%2061131--3-Structured%20Text-blue)
![IDE](https://img.shields.io/badge/IDE-CODESYS-orange)

Automation Laboratory, MSc Automation & Control Engineering · Politecnico di Milano · Group 14

## Overview

Control software for a physical didactic elevator (ground + 3 floors) running on an industrial
**ABB AC500 PLC**. The logic was developed in CODESYS, validated on a simulator and then
deployed and tested on the real plant.

## Features

- **Dispatching**: baseline single-call (FIFO) logic and optimized **F-SCAN / elevator algorithm**
  with separate up / down call queues
- **Safety logic**: emergency stop handling, automatic door opening when an escape path is
  detected (cabin aligned with a floor), door obstacle detection
- **State-machine design** for cabin motion and door control
- I/O mapping for sensors (floor presence, door state) and actuators (cabin motor, door motors,
  call LEDs)

## Hardware

| Component | Model |
| :-- | :-- |
| CPU | ABB AC500 PM554 |
| I/O | 2 × DC532 digital I/O modules |
| Plant | Didactic lift: cabin motor, 4 door motors, floor and door sensors, call buttons, LEDs |

## Tech Stack

IEC 61131-3 · Structured Text · CODESYS · ABB AC500

## Repository Structure

```
├── Elevator FINAL/                  # CODESYS project (open Elevator1_corretto.project)
├── Report Elevator Group 14.pdf     # Technical report: plant, control logics, algorithms, safety
└── README.md
```
