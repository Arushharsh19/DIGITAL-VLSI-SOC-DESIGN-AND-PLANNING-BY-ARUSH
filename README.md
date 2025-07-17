# 🚀 DIGITAL VLSI SOC DESIGN AND PLANNING  
### RTL to GDSII Workshop using Open-Source Tools (Sky130)

## 📝 Introduction

This repository contains my notes and documentation from a 5-day workshop on Digital VLSI Physical Design using open-source tools. This hands-on workshop covered the complete flow from RTL to GDSII using tools like Yosys, OpenLane, Magic, and the Sky130 PDK.


---

## 📅 Day 1: Inception of Open-Source EDA, OpenLANE and Sky130 PDK

- 🔸 [How to Talk to Computers](#how-to-talk-to-computers)
  - [Introduction to QFN-48 Package, Chip, Pads, Core, Die, and IPs](#introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
  - [Introduction to RISC-V](#introduction-to-risc-v)
  - [From Software Applications to Hardware](#from-software-applications-to-hardware)

- 🔸 [SoC Design and OpenLANE](#soc-design-and-openlane)
  - [Introduction to all components of open source digital asic design](#introduction-to-all-components-of-open-source-digital-asic-design)
  - [Simplified RTL to GDSII Flow](#simplified-rtl-to-gdsii-flow)
  - [Introduction to OpenLANE and striVe Chipsets](#introduction-to-openlane-and-strive-chipsets)
  - [Introduction to OpenLANE Detailed ASIC Design Flow](#introduction-to-openlane-detailed-asic-design-flow)

- 🔸 [Get Familiar with Open-Source EDA Tools](#get-familiar-with-open-source-eda-tools)
  - [OpenLANE Directory Structure & Linux Basics](#openlane-directory-structure--linux-basics)
  - [Design Preparation Step](#design-preparation-step-1)
  - [Files Generated After Design Prep](#files-generated-after-design-prep)
  - [Running Synthesis](#running-synthesis)
  - [Steps to Characterize Synthesis Results](#steps-to-characterize-synthesis-results)


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


---

### 🔸 SoC Design and OpenLANE

To design a digital ASIC, a few essential components and tools are needed right from the beginning:

- **RTL Design**
- **EDA Tools**
- **PDK Data**

#### 💡 What is RTL Design?

Register-Transfer Level (RTL) is a design abstraction used to model synchronous digital circuits in terms of data flow between hardware registers and the logic performed on that data.

Popular open-source RTL design sources include:
- [librecores.org](https://librecores.org)
- [opencores.org](https://opencores.org)
- GitHub repositories

#### 🧰 What are EDA Tools?

Electronic Design Automation (EDA) refers to tools used for the design and verification of ICs, PCBs, and electronic systems.

Some open-source EDA tools are:
- Qflow
- OpenROAD
- OpenLANE

#### 🧪 What is PDK Data?

PDK (Process Design Kit) is the interface between the fabrication facility (FAB) and the designer. It includes:

- Design rules (DRC, LVS, REX)
- Standard cell libraries
- I/O libraries, etc.

In 2020, Google released an open-source 130nm PDK with SkyWater Technology — suitable for many applications that don’t require advanced nodes (e.g., 5nm). 130nm processors remain performant and cost-effective.

Examples:
- Intel P4EE @3.46 GHz (Q4'04)
- sky130_OSU RV32i (pipeline version) > 1GHz

---

### 🔁 Simplified RTL to GDSII Flow

<img width="891" height="497" alt="Screenshot 2025-07-17 145305" src="https://github.com/user-attachments/assets/bd987826-1a5a-4d51-9320-bc3d2420b9b3" />


#### Step 1: Synthesis
Converts RTL to gate-level netlist using standard cell libraries. Output is functionally equivalent to RTL.



#### Step 2: Floor / Power Planning
Defines chip area, partitions blocks, and builds a power network with vertical and horizontal metal strips. Uses thicker upper metal layers to reduce resistance and combat electromigration.

<img width="452" height="203" alt="Screenshot 2025-07-17 145419" src="https://github.com/user-attachments/assets/a9fe4eef-2d09-425d-85eb-4dafe0a6d1ad" />
<img width="537" height="144" alt="Screenshot 2025-07-17 145443" src="https://github.com/user-attachments/assets/c85b8443-a7e5-480e-8ba2-4694c1006826" />



#### Step 3: Placement
Places netlist cells on defined chip rows.

- **Global Placement**: Initial rough placement optimizing congestion and timing.
- **Detailed Placement**: Precise cell positioning with constraints.

<img width="530" height="201" alt="Screenshot 2025-07-17 145511" src="https://github.com/user-attachments/assets/f507528b-ebe3-476e-b783-feddbbd3b4af" />


#### Step 4: Clock Tree Synthesis (CTS)
Routes the clock to every sequential element like flip-flops and registers. Clock networks are typically in tree shapes (H-tree, X-tree) to reduce skew.


<img width="169" height="134" alt="Screenshot 2025-07-17 145526" src="https://github.com/user-attachments/assets/bb200645-1f06-4ef8-8b45-1c44f7b639cf" />

#### Step 5: Signal Routing
Physically connects signal pins using 6 metal layers defined by the Sky130 PDK.

Types:
- Global Routing
- Detailed Routing

<img width="506" height="194" alt="Screenshot 2025-07-17 145546" src="https://github.com/user-attachments/assets/1554872d-e5ee-44df-8d62-afc9f3d16779" />


#### Step 6: Sign-Off
Includes final verification steps:

- **Physical Verification** (DRC, LVS)
- **Timing Verification** (Static Timing Analysis)

---

### 🔸 Introduction to OpenLANE and striVe Chipsets

**OpenLANE** is an automated RTL to GDSII flow that integrates multiple tools like:
- OpenROAD
- Yosys
- Magic
- Netgen
- Klayout, etc.

It aims to produce **clean GDSII output** with:
- ❌ No LVS violations
- ❌ No DRC violations
- ❌ No timing violations

🧪 Modes:
- **Autonomous**: Push-button full flow
- **Interactive**: Step-by-step manual control

**striVe** is a family of fully open-source SoCs including:
- Open PDK
- Open EDA
- Open RTL

<img width="837" height="466" alt="Screenshot 2025-07-17 145732" src="https://github.com/user-attachments/assets/b1fcfdca-a2b1-4693-a44f-108d70315ef8" />


---

### 🔸 Introduction to OpenLANE Detailed ASIC Design Flow

OpenLANE supports over 43 design examples. It also supports:

- DFT (Design for Test)
- Scan insertion
- Fault simulation
- Physical Implementation using OpenROAD

Steps include:
- Floor/Power Planning
- Tap Cell and Decap insertion
- Placement (Global and Detailed)
- CTS
- Routing
- Post-placement optimization
  
<img width="857" height="476" alt="Screenshot 2025-07-17 145947" src="https://github.com/user-attachments/assets/d46d02ad-3435-425f-8e30-66468daf0232" />

Every netlist modification step is followed by **functional verification using LCE (Yosys)**.

#### ⚠️ Dealing with Antenna Rule Violations

Wires can act like antennas and damage gates. Solutions:
1. **Bridging**: Connects to higher metal layer
2. **Antenna Diode Cells**: Leaks away charge

<img width="411" height="206" alt="Screenshot 2025-07-17 150017" src="https://github.com/user-attachments/assets/b2cdf3cb-de08-4cb4-b40b-25d299888814" />


In OpenLANE, **fake antenna diodes** are added first and replaced with real ones if needed after violation checking.

<img width="543" height="206" alt="Screenshot 2025-07-17 150030" src="https://github.com/user-attachments/assets/415b9052-1a0c-4e82-84a3-a7152c4c956a" />
<img width="256" height="199" alt="Screenshot 2025-07-17 150047" src="https://github.com/user-attachments/assets/925dc622-12df-4631-aff4-b83e9eca1645" />


#### ⏱️ Static Timing Analysis (STA)

Uses `DEF2SPEF` to extract RC data from routed layout and runs **STA** using OpenSTA (OpenROAD).

#### 🧪 Physical Verification

- **DRC**: Checked using Magic
- **LVS**: Done via Magic + Netgen

---

### 🔸 Get Familiar with Open-Source EDA Tools

#### 📁 OpenLANE Directory Structure & Linux Basics

Useful commands:
- `cd` – Change directory
- `ls` – List files
- `pwd` – Show working directory
- `mkdir` – Create new directory
- `command --help` – Help menu
- `clear` – Clear screen

We are using:  
**sky130_fd_sc_hd**  
- `sky130`: Process node  
- `fd`: Foundry  
- `sc`: Standard Cell  
- `hd`: High Density

This variant includes:
- verilog, spice, techlef, meglef, mag, gds, cdl, lib, lef, etc.

---

### 🔧 Design Preparation Step

In OpenLANE, we use the `flow.tcl` script. Running with `-interactive` allows step-by-step execution.

<img width="954" height="925" alt="Screenshot 2025-07-17 152021" src="https://github.com/user-attachments/assets/0e81fc19-d1a5-4b23-886b-9c9a940e565a" />


### 🛠️ Design Preparation Step

Once inside the OpenLANE environment, the flow is controlled using the `flow.tcl` script. This script automates the entire ASIC design process. By using the `-interactive` switch, we can perform each stage manually, allowing more control and understanding. Without the `-interactive` switch, OpenLANE will execute the complete RTL to GDSII flow in one go.

Once OpenLANE is launched interactively, the prompt changes to indicate that we are now inside the OpenLANE shell.



Next, we load all the required packages necessary to run the OpenLANE flow.

<img width="954" height="1013" alt="Screenshot 2025-07-17 152024" src="https://github.com/user-attachments/assets/d06ccbd6-6749-497e-87a6-58c8438dcdbd" />

Now we are ready to execute our first command.

---

### 📂 Design Folder Overview

Inside the OpenLANE `designs` directory, we have access to 30–40 pre-built designs. For this workshop, we use the design named `picorv32a`. Upon entering the `picorv32a` folder, you will find several files, including scripts and configuration files like `config.tcl`.

The `config.tcl` file defines important design parameters such as clock period, I/O configurations, and design constraints.

<img width="955" height="1013" alt="Screenshot 2025-07-17 151953" src="https://github.com/user-attachments/assets/cd0f42c7-9c87-495f-a1a9-ce2ba40db977" />


In this example, the time period is set to `5.00 ns` in the `config.tcl` file. However, in the global configuration (`sky130_fd_sc_hd`), it may be set to `24 ns`. If both exist, the local `config.tcl` takes priority, overriding the global setting.

---

### ⚙️ Preparing the Design for Flow

Before synthesis, we must prepare the design using the following command:

```tcl
prep -design picorv32a
```
<img width="948" height="1012" alt="Screenshot 2025-07-17 152132" src="https://github.com/user-attachments/assets/1011415c-727f-4241-a43c-b00ee356f17a" />

This sets up the environment for the selected design.

Once preparation is complete, a `runs` directory is created under `picorv32a`, timestamped with the current date. This directory contains several subfolders used throughout the design flow.

<img width="956" height="1016" alt="Screenshot 2025-07-17 152332" src="https://github.com/user-attachments/assets/4b3a897c-61a3-4d76-9c63-e7c63ff5fb7e" />


---

### 📁 Files Generated After Design Prep

Inside the `temp` folder, a file named `merged.lef` is generated. It includes wiring, layer-level, and cell-level information.
<img width="961" height="1014" alt="Screenshot 2025-07-17 152439" src="https://github.com/user-attachments/assets/5c3db019-56ab-40e2-a3dd-2a37131dd061" />

The `results` folder is initially empty, as no stages have been executed yet.

The `reports` folder contains predefined directories for:
- Synthesis
- Placement
- Floorplanning
- CTS
- Routing
- Magic
- LVS

A new `config.tcl` is also generated here, containing the default parameters taken by the flow. Changes made to the original config file will reflect here once we rerun specific stages.

> 🔄 Example: If you modify the `core_utilization` parameter before floorplanning and re-execute that step, the changes will be reflected in the new `config.tcl` file.

---

### 🔧 Running Synthesis

To perform synthesis, run:

```tcl
run_synthesis
```
<img width="956" height="1017" alt="Screenshot 2025-07-17 152529" src="https://github.com/user-attachments/assets/569d2833-1b98-4392-8c8c-5569ff0bfc31" />

This step typically takes 3–4 minutes to complete. Once complete, the flow has performed logic optimization and technology mapping.
<img width="958" height="1013" alt="Screenshot 2025-07-17 152605" src="https://github.com/user-attachments/assets/7bc34a23-4656-4c2d-9c29-0e993b804020" />

---

### 📊 Steps to Characterize Synthesis Results

After synthesis is complete, you can review the following:

- **Number of D flip-flops**: 1613  
- **Total number of cells**: 14,876  
<img width="953" height="1017" alt="Screenshot 2025-07-17 153034" src="https://github.com/user-attachments/assets/9874eb2c-1270-42fe-a17e-9771fb8201e1" />

The **Flop Ratio** is calculated as:

```text
Flop Ratio = (Number of Flip-Flops) / (Total Number of Cells)
           = 1613 / 14876
           = 10.84%
```

Before synthesis, the `results` folder was empty. Now it contains all mapping data generated by **ABC** (AIG-based logic synthesis and optimization tool).
<img width="953" height="1019" alt="Screenshot 2025-07-17 152924" src="https://github.com/user-attachments/assets/3384db63-3502-4710-b8de-34ca290bbaa3" />

Inside the `reports/synthesis` folder, you will find detailed statistics and logs indicating:

- Exact timing
- Logic utilization
- Cell statistics
- Resource usage
<img width="961" height="1019" alt="Screenshot 2025-07-17 153236" src="https://github.com/user-attachments/assets/49a47d34-dcf5-4b11-8135-ac3440d53a02" />

These match the figures we've just reviewed.

---
