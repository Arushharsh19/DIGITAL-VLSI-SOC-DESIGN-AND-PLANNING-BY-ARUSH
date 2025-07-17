# 🚀 DIGITAL VLSI SOC DESIGN AND PLANNING  
### RTL to GDSII Workshop using Open-Source Tools (Sky130)

## 📝 Introduction

This repository contains my notes and documentation from a 5-day workshop on Digital VLSI Physical Design using open-source tools. This hands-on workshop covered the complete flow from RTL to GDSII using tools like Yosys, OpenLane, Magic, and the Sky130 PDK.


---

## 📅 Day 1: Inception of Open-Source EDA, OpenLANE and Sky130 PDK

### 🔸 How to talk to computers
- Introduction to QFN-48 Package, chip, pads, core, die and IPs
- Introduction to RISC-V
- From Software Applications to Hardware

### 🔸 SoC Design and OpenLANE
- Introduction to all components of open-source digital ASIC design
- Simplified RTL2GDS flow
- Introduction to OpenLANE and Strive chipsets
- Introduction to OpenLANE detailed ASIC design flow

### 🔸 Get familiar with Open-Source EDA Tools
- OpenLANE Directory structure in detail
- Design Preparation Step
- Review files after design prep and run synthesis
- OpenLANE Project Git Link Description
- Steps to characterize synthesis results

---

## 📅 Day 2: Good Floorplanning Considerations

### 🔸 Chip Floorplanning Consideration
- Utilization factor and aspect ratio
- Concept of pre-placed cells
- De-coupling capacitors
- Power planning
- Pin placement and logical cell placement blockage
- Steps to run floorplan using OpenLANE
- Review floorplan files and steps to view floorplan
- Review floorplan layout in Magic

### 🔸 Library Building and Placement
- Netlist binding and initial place design
- Optimize placement using estimated wire-length and capacitance
- Final placement optimization
- Need for libraries and characterization
- Congestion aware placement using RePlAce

### 🔸 Cell Design and Characterization Flows
- Inputs for cell design flow
- Circuit design steps
- Layout design step
- Typical characterization flow

### 🔸 General Timing Characterization Parameters
- Timing threshold definitions
- Propagation delay and transition time

---

## 📅 Day 3: Design Library Cell using Magic Layout and ngspice Characterization

### 🔸 Labs for CMOS Inverter ngspice Simulations
- IO placer revision
- SPICE deck creation for CMOS inverter
- SPICE simulation lab for CMOS inverter
- Switching Threshold Vm
- Static and dynamic simulation of CMOS inverter
- Lab steps to git clone `vsdstdcelldesign`

### 🔸 Inception of Layout – CMOS Fabrication Process
- Create Active regions
- Formation of N-well and P-well
- Formation of gate terminal
- Lightly doped drain (LDD) formation
- Source & drain formation
- Local interconnect formation
- Higher level metal formation
- Layout and LEF using inverter

### 🔸 Sky130 Tech File Labs
- Create final SPICE deck using Sky130 tech
- Characterize inverter using Sky130 model files
- Magic tool options and DRC rules
- Steps to download labs and load Sky130 tech-rules
- Fix `poly.9` DRC error in tech-file
- Implement poly resistor spacing to diff and tap
- Describe DRC error as geometrical construct
- Identify and fix missing/incorrect DRC rules

---

## 📅 Day 4: Pre-Layout Timing Analysis and Importance of Good Clock Tree

### 🔸 Timing Modeling using Delay Tables
- Convert grid info to track info
- Convert Magic layout to std cell LEF
- Include new cell in synthesis
- Introduction to delay tables (part 1 & 2)
- Fix slack and include `vsdinv` cell in synthesis

### 🔸 Timing Analysis with Ideal Clocks using OpenSTA
- Flip-flop setup time and clock uncertainty
- Configure OpenSTA for post-synth timing analysis
- Optimize synthesis to reduce setup violations
- Perform basic timing ECO

### 🔸 Clock Tree Synthesis (CTS) using TritonCTS
- H-Tree based routing and buffering
- Crosstalk and clock net shielding
- Run and verify CTS using TritonCTS

### 🔸 Timing Analysis with Real Clock using OpenSTA
- Setup and hold timing analysis with real clock
- Execute OpenSTA with correct timing libraries
- Observe impact of CTS buffers on timing

---

## 📅 Day 5: Final Steps for RTL2GDS using TritonRoute and OpenSTA

### 🔸 Routing and Design Rule Check (DRC)
- Maze Routing and Lee’s Algorithm
- Importance of Design Rule Check (DRC)

### 🔸 Power Distribution Network and Routing
- Build power distribution network
- Connect power straps to std cell power
- Global and detailed routing using TritonRoute

### 🔸 TritonRoute Features
- Pre-processed route guide handling
- Inter-guide connectivity and routing layers
- Handling connectivity with routing topology algorithms
- Final output files after routing

---

## 📅 Day 1: Inception of Open-Source EDA, OpenLANE and Sky130 PDK

### 🔸 How to Talk to Computers?

To understand how we interact with hardware, let’s begin with a familiar device — the **Arduino board**.

This board has a small **microcontroller chip** at its center (highlighted in the image below), which acts as the "brain" of the system. Every input/output component on the board communicates with this chip.

🧠 The journey of designing this chip — from a high-level idea down to physical manufacturing — is known as the **RTL to GDSII flow**.

Arduino, as a platform, includes both:
- A programmable circuit board (hardware), and
- An IDE (Integrated Development Environment) to write and upload code to the board (software).

![arduino-leonardo-board](https://github.com/user-attachments/assets/962acef5-4981-4989-a563-5be46bdf3c4d)

---

### 🧩 Introduction to QFN-48 Package, Chip, Pads, Core, Die, and IPs

A modern chip, especially something like a microcontroller or a processor, is typically packaged in formats such as **QFN-48 (Quad Flat No-lead)**. Inside such a chip package, there are several components:

- **Pads**: Points where external pins connect to the internal silicon.
- **Core**: The main logic area where all gates and circuits are implemented.
- **Die**: The actual piece of silicon that houses the core and other components.

In a chip like one based on **RISC-V**, you may find components like:
- SRAM
- SoC Blocks
- ADC, DAC
- SPI

These are often provided as **Foundry IPs** — pre-designed blocks offered by the fabrication facility.

Foundries use advanced processes such as **deposition**, **etching**, and **photolithography** to turn circuit designs into physical chips.

<img width="725" height="400" alt="Screenshot 2025-07-17 144340" src="https://github.com/user-attachments/assets/a310e062-215c-454a-8a32-ce07ad860481" />


---

### 🔸 Introduction to RISC-V

**RISC-V** (pronounced “risk-five”) is an open and free-to-use Instruction Set Architecture (ISA) that originated at the **University of California, Berkeley**. The “V” in RISC-V stands for the **fifth generation** of RISC design.

It is gaining popularity due to several advantages:
- ✅ Completely open-source — no licensing costs
- ✅ Modular — supports custom extensions
- ✅ Scalable — available in 32-bit, 64-bit, and even experimental 128-bit versions
- ✅ Backed by both academia and industry

Physically, the **die** inside a chip is connected to the external pins using **bond wires**. These wires serve as bridges between the internal circuits and the outside world.

<img width="721" height="401" alt="Screenshot 2025-07-17 144900" src="https://github.com/user-attachments/assets/bb78d8a2-b800-4555-8664-68cf636af731" />


---

### 🔸 From Software Applications to Hardware

Ever wondered how apps like WhatsApp, Instagram, or games work at a hardware level? Let’s break it down.

All application software runs on top of system software, which then interacts with the hardware chip. So, the full stack looks like this:  
**Application Software → System Software → Hardware Chip**

Here’s what each part does:

- **Operating System (OS)**: Manages memory, I/O devices, and processes.
- **Compiler**: Converts high-level programming languages like C/C++ into low-level machine instructions.
- **Assembler**: Further translates those instructions into binary — the 0s and 1s understood by hardware.

These binary instructions are what ultimately communicate with the chip to make software work on physical devices.

<img width="886" height="495" alt="Screenshot 2025-07-17 145151" src="https://github.com/user-attachments/assets/90edbf10-f7c6-4487-af4e-604f6378afa3" />

