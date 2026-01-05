# 🏢 Automation of an Elevator Plant (IEC 61131-3)

![PLC](https://img.shields.io/badge/PLC-ABB_AC500-red)
![Language](https://img.shields.io/badge/Language-Structured_Text_(ST)-blue)
![IDE](https://img.shields.io/badge/IDE-CODESYS_v2.3-orange)
![Course](https://img.shields.io/badge/Course-Automation_Laboratory-green)

> **Group Project** | MSc Automation and Control Engineering | Politecnico di Milano  
> *Design, simulation, and implementation of a control logic for a 4-floor elevator plant using industrial PLCs.* [file:12]

## 🎯 Objective
To develop a robust, modular, and safe control system for a multi-floor elevator (Didactic Lift ASC89) using an **ABB AC500 PLC**. The project moves beyond basic relay logic to implement optimized dispatching algorithms that minimize average waiting times and energy consumption. The system was validated through both a virtual digital twin in CODESYS and the physical plant.

## 🔧 System Architecture

### Hardware Specifications
*   **Plant:** 4-floor didactic elevator (Ground + 3 floors) with independent DC motors for cabin and doors.
*   **Controller:** ABB PM554 PLC (128kB) with 2x DC532 Digital I/O Modules.
*   **Sensors:** 4x Cabin presence sensors (limit switches), 8x Door state sensors (open/closed), Cabin obstacle detection.
*   **Actuators:** Bi-directional cabin motor, 4x Door motors, 12+ LED indicators. [file:12]

### Software Architecture (Finite State Machines)
The control logic is modelled using deterministic Finite State Machines (FSM) to ensure safety and predictability:
1.  **Elevator Model:** 7 States (4 floors + 3 inter-floor transit states).
2.  **Door Model:** 4 States (Open, Opening, Closed, Closing) with obstacle interrupt logic.
3.  **Supervisor:** Manages global state transitions, priority tasks (Emergency), and I/O mapping.

## 📊 Algorithms & Control Strategies

### 1. Single Call Logic (FIFO)
A baseline approach where requests are served sequentially in the order of arrival.
*   **Pros:** Simple implementation, deterministic.
*   **Cons:** Inefficient for high traffic; high cumulative travel distance.

### 2. Optimized Dispatching (SCAN / Elevator Algorithm)
We implemented the **F-SCAN algorithm** (commonly used in disk scheduling) to optimize multiple simultaneous calls.
*   **Logic:** The cabin continues in the current direction (e.g., UP) as long as there are pending requests in that direction. It only reverses direction when the "highest" or "lowest" active call is reached.
*   **Queuing System:**
    *   `Queue_Cab`: Circular buffer for internal cabin calls (max 4).
    *   `Queue_Floor`: Split arrays for Up-calls and Down-calls to prioritize direction-matching requests.
*   **Benefit:** drastically reduces "starvation" of requests and total motor runtime. [file:12]

### 3. Safety & Emergency Protocols
Safety is handled via a **Preemptive Task** with higher priority:
*   **Emergency Stop:** Immediate motor cutoff and engagement of braking system.
*   **Escape Path:** If stopped at a floor alignment ($\pm$ tolerance window), doors automatically open to allow passenger egress.
*   **Obstacle Detection:** Immediate reversal of door motor torque upon sensor activation. [file:12]

## 📂 Repository Structure
```bash
├── src/
│   ├── Main_PRG.st        # Core logic loop
│   ├── SCAN_Algorithm.st  # Dispatching logic (SCAN/LOOK)
│   ├── FSM_Door.st        # Door state machine
│   ├── Safety.st          # Emergency handling
│   └── Drivers.st         # I/O mapping (DATA_IN/OUT)
├── docs/
│   └── Report_Elevator_Group14.pdf  # Full technical report
├── visualization/
│   └── HMI_CODESYS.png    # Virtual plant interface
└── README.md
