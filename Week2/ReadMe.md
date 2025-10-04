---

# 🌟 VSDBabySoC – Fundamentals of System-on-Chip (SoC) Design

<div align="center">

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![RISC-V](https://img.shields.io/badge/Architecture-RISC--V-orange?style=flat-square)](https://riscv.org/)
[![Sky130](https://img.shields.io/badge/Process-Sky130-green)](https://skywater-pdk.readthedocs.io/)

</div>

---

## 📚 Table of Contents

1. [Introduction](#introduction)
2. [Understanding SoC](#understanding-soc)

   * [Why SoCs?](#why-socs)
   * [Components of SoC](#components-of-soc)
   * [Types of SoCs](#types-of-socs)
3. [SoC Design Flow](#soc-design-flow)
4. [VSDBabySoC – Overview](#vsdbabysoc--overview)

   * [Key Features](#key-features)
   * [Architecture](#architecture)
5. [Setup & Environment](#setup--environment)
6. [Simulation Workflow](#simulation-workflow)
7. [Instruction Program Example](#instruction-program-example)
8. [Learning Outcomes](#learning-outcomes)
9. [Future Enhancements](#future-enhancements)
10. [References](#references)

---

## 🌟 Introduction

**VSDBabySoC** is a **learning-focused RISC-V System-on-Chip (SoC)** that demonstrates the fundamentals of modern chip design in a simplified form. Built around the **RVMYTH CPU core**, it integrates:

* ⏱ **Phase-Locked Loop (PLL)** – for stable clock generation
* 🎚 **10-bit Digital-to-Analog Converter (DAC)** – for digital-to-analog interfacing

The purpose of this project is to **bridge theory and practice**, providing a platform where learners can explore:

* CPU instruction execution
* Clock synchronization challenges
* Digital-to-analog conversion
* SoC functional modeling and verification

---

## 🧐 Understanding SoC

A **System-on-Chip (SoC)** is like a **mini-computer on a single silicon chip**. It integrates computing, memory, communication, and special-purpose units into one compact and efficient design.

### ⚡ Why SoCs?

| Feature              | Why it Matters 🚀                                     |
| -------------------- | ----------------------------------------------------- |
| **Compactness**      | Enables smaller devices (smartphones, wearables, IoT) |
| **Energy Efficient** | On-chip communication saves power                     |
| **Performance**      | High-speed, low-latency data paths                    |
| **Cost Reduction**   | Fewer discrete ICs → cheaper manufacturing            |
| **Reliability**      | Fewer failure points                                  |

**Real-world Applications:**
📱 Smartphones, ⌚ Wearables, 🚗 Automotive ECUs, 🏠 IoT Smart Devices

---

### 🧩 Components of SoC

1. **CPU (Central Processing Unit):** Executes instructions and manages system control.

   * In BabySoC → RVMYTH CPU (RISC-V)
2. **Memory:** Stores data and programs (RAM, ROM, Flash).
3. **I/O Interfaces:** Communicate with peripherals (UART, SPI, GPIO, USB).
4. **PLL (Clock Management):** Generates stable system clocks.
5. **DAC/ADC:** Convert between digital and analog domains.
6. **Optional Components:** GPU, DSP, PMU, Wireless Modules.

💡 **Analogy:**
Think of an SoC as a **city** – CPU is the **city hall**, memory is the **library**, I/O are the **roads**, PLL is the **clock tower**, and DAC/ADC are the **translators**.

---

### 🔥 Types of SoCs

1. **Microcontroller SoCs** – Simple, low-power (IoT, appliances).
2. **Microprocessor SoCs** – OS support, multitasking (smartphones, tablets).
3. **Application-Specific SoCs (ASICs)** – Optimized for AI, graphics, networking.

🍼 **VSDBabySoC** belongs to category 2 (microprocessor-style), but simplified for education.

---

## 🌀 SoC Design Flow

1. **Functional Modeling** – Simulate system behavior (abstract level).
2. **RTL Design** – Hardware description in Verilog/TLV.
3. **Synthesis** – Translate RTL into gate-level design.
4. **Physical Design** – Place & route (Sky130 fabrication-ready).

VSDBabySoC focuses heavily on **functional modeling** → early testing before RTL complexity.

---

## 👶 VSDBabySoC – Overview

### 🔑 Key Features

* RVMYTH RISC-V CPU Core
* 8× PLL for clock generation
* 10-bit DAC for analog output
* Instruction-driven DAC waveform generation
* Open-source & documented

---

### 🧩 Architecture

**Block Diagram (Simplified):**

```
[ Instruction Memory ] → [ RVMYTH CPU ] → r17 → [ 10-bit DAC ] → Analog OUT
                                ↑
                                |
                               [PLL]
```

| Component | Function                                    |
| --------- | ------------------------------------------- |
| **CPU**   | Executes instructions, updates DAC register |
| **PLL**   | Generates stable high-frequency clock       |
| **DAC**   | Converts 10-bit digital → analog output     |

💡 **Analogy:**
CPU = Brain 🧠 | PLL = Heartbeat ❤️ | DAC = Voice 🔊

---

## ⚙️ Setup & Environment

### Clone the Repository

```bash
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC
```

### Install Dependencies

```bash
sudo apt update
sudo apt install python3-venv python3-pip iverilog gtkwave
python3 -m venv sp_env
source sp_env/bin/activate
pip install pyyaml click sandpiper-saas
```

### Convert TL-Verilog → Verilog

```bash
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```

---

## 🧪 Simulation Workflow

### Pre-Synthesis Simulation

```bash
mkdir -p output/pre_synth_sim
iverilog -o output/pre_synth_sim/pre_synth_sim.out \
  -DPRE_SYNTH_SIM \
  -I src/include -I src/module \
  src/module/testbench.v

cd output/pre_synth_sim
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```

### Key Signals to Monitor

| Signal      | Description                       |
| ----------- | --------------------------------- |
| `CLK`       | System clock (from PLL)           |
| `reset`     | Reset signal                      |
| `OUT`       | DAC output waveform               |
| `RV_TO_DAC` | Data path from CPU register → DAC |

---

## 🔄 Instruction Program Example

| Step | Instruction        | Action              |
| ---- | ------------------ | ------------------- |
| 0    | `ADDI r9, r0, 1`   | Initialize constant |
| 1    | `ADDI r10, r0, 43` | Loop limit = 43     |
| 2    | `ADDI r11, r0, 0`  | Counter reset       |
| 3    | `ADDI r17, r0, 0`  | DAC input = 0       |
| …    | …                  | …                   |
| 12   | `BEQ r0, r0, ...`  | Infinite loop       |

**DAC Output Formula:**
The DAC output voltage is given by:  

$V_{OUT} = \dfrac{r17}{1023} \times V_{REF}$

Example: If `r17 = 512`, `VOUT ≈ 0.5 × VREF`.

---

## 🎯 Learning Outcomes

By working with **VSDBabySoC**, learners gain:

✔ Understanding of SoC components (CPU, PLL, DAC)
✔ Hands-on with **functional modeling** & simulation
✔ Basics of **clock synchronization**
✔ Fundamentals of **digital-to-analog conversion**
✔ Exposure to **RISC-V instruction execution**

---

## 🚀 Future Enhancements

* Add instruction memory to load C programs
* Expand peripheral support (ADC, UART, GPIO)
* Implement a waveform generator example via DAC
* Enable full RTL-to-GDSII flow with Sky130

---

## 📚 References

* [RISC-V ISA Specifications](https://riscv.org/specifications/)
* [SkyWater Sky130 PDK](https://skywater-pdk.readthedocs.io/)
* Harris & Weste – *CMOS VLSI Design*
* [TL-Verilog & Sandpiper-SaaS](https://www.redwoodeda.com/)

---