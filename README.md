# PLC Control of a 4-Floor Elevator

**Automation Laboratory · MSc Politecnico di Milano · group project**

Control software for a real didactic elevator (4 floors, cabin and door motors, presence and
door sensors), running on an **industrial ABB PLC**. Developed and tested first on a simulator,
then on the physical plant.

## Highlights

- **Two dispatching logics**: a simple single-call (FIFO) version, then an optimised
  **F-SCAN / elevator algorithm** with separate up/down call queues, so the cabin keeps its
  direction while there are pending calls
- **Safety first**: emergency stop handling, automatic door opening when the cabin is aligned
  with a floor (escape path), obstacle detection on the doors
- **State-machine design** for cabin and doors

## Hardware

- ABB AC500 PLC (PM554 CPU) with 2× DC532 digital I/O modules
- Didactic lift with cabin motor, 4 door motors, floor and door sensors, call buttons and LEDs

## Stack

IEC 61131-3 · Structured Text · CODESYS · ABB AC500

## Files

| File | Content |
| :-- | :-- |
| [`Report Elevator Group 14.pdf`](Report%20Elevator%20Group%2014.pdf) | Full technical report: plant, logics, algorithms, safety |
| [`Elevator FINAL/`](Elevator%20FINAL) | CODESYS project (open `Elevator1_corretto.project`) |
