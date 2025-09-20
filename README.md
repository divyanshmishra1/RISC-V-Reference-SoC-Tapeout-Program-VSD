
# 🖥️ RISC-V SoC Tapeout Program VSD

<div align="center">

![RISC-V](https://img.shields.io/badge/RISC--V-SoC%20Tapeout-blue?style=for-the-badge&logo=riscv)
![VSD](https://img.shields.io/badge/VSD-Program-orange?style=for-the-badge)
![Participants](https://img.shields.io/badge/Participants-3500+-success?style=for-the-badge)
![India](https://img.shields.io/badge/Made%20in-India-saffron?style=for-the-badge)

</div>

Welcome to my journey through the **RISC-V SoC Tapeout Program (VSD)**!  

This repository documents my **Week 0 progress**, including GitHub setup, tool installations, and verification proofs.

<div align="center">

> *"Hands-on journey from RTL design to tapeout using open-source EDA tools while contributing to India’s RISC-V ecosystem."*

</div>

<div align="center">

```

📝 RTL Design → 🔄 Synthesis → 📊 Simulation → ⚡ Verification

```

</div>

---

## 📅 Week 0 — Overview

This week focuses on:

 **Task:** Installing and verifying core EDA tools for RTL design and simulation.

---


</details>

<details>
<summary><b>🛠️ Task: Tool Installation</b></summary>

**System Requirements:**

| Parameter | Requirement       |
| --------- | ----------------- |
| RAM       | 6 GB              |
| HDD       | 50 GB             |
| OS        | Ubuntu 20.04+     |
| CPU       | 4 vCPU            |
| VM        | Oracle VirtualBox |

---

### 📦 Tools Installed

| Tool            | Purpose                            | Verification |
| --------------- | ---------------------------------- | ------------ |
| 🧠 **Yosys**    | RTL Synthesis & Logic Optimization | ✅ Verified   |
| 📟 **Iverilog** | Verilog Simulation & Compilation   | ✅ Verified   |
| 📊 **GTKWave**  | Waveform Viewer & Analysis         | ✅ Verified   |
| ⚡ **Ngspice**   | Analog & Mixed-Signal Simulation   | ✅ Verified   |

---

#### 1️⃣ Yosys (RTL Synthesis)

```bash
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get install build-essential clang bison flex \
libreadline-dev gawk tcl-dev libffi-dev git \
graphviz xdot pkg-config python3 libboost-system-dev \
libboost-python-dev libboost-filesystem-dev zlib1g-dev
git submodule update --init --recursive
make config-gcc
make
sudo make install
```

**Proof:**
![Yosys Installation](Screenshots/yosys.png)

---

#### 2️⃣ Iverilog (Verilog Simulation)

```bash
sudo apt-get update
sudo apt-get install iverilog
iverilog -v
```

**Proof:**
![Iverilog Verification](Screenshots/iverilog.png)

---

#### 3️⃣ GTKWave (Waveform Viewer)

```bash
sudo apt-get update
sudo apt install gtkwave
gtkwave --version
```

**Proof:**
![GTKWave Verification](Screenshots/gtkwave.png)

---

#### 4️⃣ Ngspice (Analog & Mixed-Signal Simulation)

```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure --with-x --with-readline=yes --disable-debug
make
sudo make install
```

**Proof:**
![NGSpice Verification](Screenshots/ngspice.png)

---

### 🌟 Key Learnings from Week 0

* **Successfully installed** and verified core open-source EDA tools.
* **Configured environment** for RTL design, simulation, and synthesis.
* **Prepared system** for upcoming RTL-to-GDSII experiments.
* Learned **dependency management** and professional workflow setup.

</details>

---

## 📈 Weekly Progress Tracker

![Week 0](https://img.shields.io/badge/Week%200-Tools%20Setup-success?style=flat-square)
![Week 1](https://img.shields.io/badge/Week%201-Coming%20Soon-lightgrey?style=flat-square)
![Week 2](https://img.shields.io/badge/Week%202-Upcoming-lightgrey?style=flat-square)

---

````
