# 3-Bit Binary Multiplier Using Basic Logic Gates

![Course](https://img.shields.io/badge/Course-Digital%20Electronics-blue)
![University](https://img.shields.io/badge/University-HUST-red)
![Simulation](https://img.shields.io/badge/Simulation-Proteus%208-green)
![Hardware](https://img.shields.io/badge/Hardware-74HC%20Series%20ICs-orange)

A gate-level hardware design, simulation, and breadboard implementation of an unsigned **3-bit binary multiplier** built exclusively from fundamental `AND`, `OR`, and `XOR` logic gates—without relying on dedicated adder ICs (such as the 74LS83).

Developed as a Course Project for **Digital Electronics ** at the **School of Electrical and Electronic Engineering, Hanoi University of Science and Technology (HUST)**.

---

## 📋 Table of Contents
- [Overview](#-overview)
- [Circuit Architecture](#-circuit-architecture)
- [Bill of Materials (BOM)](#-bill-of-materials-bom)
- [Simulation & Hardware Results](#-simulation--hardware-results)
- [Project Structure](#-project-structure)
- [Limitations & Future Work](#-limitations--future-work)
- [Team & Acknowledgments](#-team--acknowledgments)

---

## 🔍 Overview

The multiplier computes the product of two 3-bit unsigned binary numbers, $A = (A_2 A_1 A_0)_2$ and $B = (B_2 B_1 B_0)_2$, where each operand ranges from $0$ to $7$ ($000_2$ to $111_2$). 

Because the maximum product is $7 \times 7 = 49_{10}$ ($110001_2$), the circuit produces a **6-bit output** $P = (P_5 P_4 P_3 P_2 P_1 P_0)_2$.

### Key Features
* **100% Gate-Level Design:** Constructs Full Adders from scratch using discrete `XOR`, `AND`, and `OR` gates.
* **Verified in Simulation:** Fully modeled and tested in **Proteus 8 Design Suite**.
* **Physical Prototype:** Assembled and verified on a solderless breadboard using standard 74HC-series CMOS ICs and LED indicators.

---

## ⚙️ Circuit Architecture

### 1. Partial Product Generation
Nine 2-input `AND` gates compute all bit-wise partial products ($A_i \cdot B_j$) in parallel:

```text
          A2   A1   A0
       ×  B2   B1   B0
       ----------------
        A2B0 A1B0 A0B0
   A2B1 A1B1 A0B1
A2B2 A1B2 A0B2
-----------------------
P5   P4   P3   P2   P1   P0
```

### 2. Gate-Level Full Adder Design
Instead of using a 4-bit binary adder IC, three independent **Full Adders** were built from basic logic gates (5 gates per Full Adder):
* **Sum:** $S = A \oplus B \oplus C_{in}$
* **Carry-out:** $C_{out} = (A \cdot B) + C_{in} \cdot (A \oplus B)$

*(Tip: Place your Proteus schematic image in `docs/schematic.png` and uncomment the line below)*
<!-- ![Proteus Schematic](docs/schematic.png) -->

---

## 🛠️ Bill of Materials (BOM)

| Component | Description | Purpose |
| :--- | :--- | :--- |
| **74HC08** | Quad 2-Input `AND` Gate IC | Partial product generation & Full Adder carry logic |
| **74HC86** | Quad 2-Input `XOR` Gate IC | Full Adder sum logic |
| **74HC32** | Quad 2-Input `OR` Gate IC | Full Adder carry-out combination |
| **LEDs (x6)** | Standard 5mm LEDs | Visual binary output ($P_5$ down to $P_0$) |
| **Breadboard & Wires** | Solderless prototype board | Hardware assembly and VCC/GND input switching |

---

## 📊 Simulation and Hardware Results

Both the **Proteus 8 simulation** and the **physical breadboard circuit** were tested across multiple input vectors and matched theoretical values with 100% accuracy:

| Operand A | Operand B | Decimal Product | Theoretical | Proteus Sim | Hardware LEDs |
| :---: | :---: | :---: | :---: | :---: | :---: |
| `001` (1) | `001` (1) | $1 \times 1 = 1$ | `000001` | `000001` | `000001` |
| `010` (2) | `011` (3) | $2 \times 3 = 6$ | `000110` | `000110` | `000110` |
| `011` (3) | `101` (5) | $3 \times 5 = 15$ | `001111` | `001111` | `001111` |
| `101` (5) | `110` (6) | $5 \times 6 = 30$ | `011110` | `011110` | `011110` |
| `111` (7) | `111` (7) | $7 \times 7 = 49$ | `110001` | `110001` | `110001` |

*(Tip: Place your breadboard photo in `docs/hardware.jpg` and uncomment the line below)*
<!-- ![Breadboard Implementation](docs/hardware.jpg) -->

---

## 📁 Project Structure

```text
├── docs/                   # Schematic diagrams, breadboard photos, and full report
│   ├── DTS-Report-VIE.docx # Original Vietnamese report
│   └── DTS-Report-ENG.md   # English translated report
├── proteus/                # Proteus 8 (.pdsprj) simulation files
└── README.md               # Project documentation
```

---

## 🚀 Limitations and Future Work

* **Wiring Complexity:** Using discrete logic gates increases wire density on a breadboard. Designing a custom **PCB** would improve reliability and compactness.
* **Fixed Bit-Width:** Currently limited to 3-bit inputs; can be scaled to a 4-bit or 8-bit array multiplier.
* **Display Output:** Adding a Binary-to-BCD converter and **7-segment displays** would allow direct decimal readout instead of manual binary reading via LEDs.

---

### References
* [Texas Instruments SNx4HC08 Datasheet](https://www.ti.com/lit/ds/symlink/sn74hc08.pdf)
* [Texas Instruments SNx4HC86 Datasheet](https://www.ti.com/lit/ds/symlink/sn74hc86.pdf)
* [Texas Instruments SNx4HC32 Datasheet](https://www.ti.com/lit/ds/symlink/sn74hc32.pdf)
