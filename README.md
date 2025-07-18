# 🚀 DIGITAL VLSI SOC DESIGN AND PLANNING  
### RTL to GDSII Workshop using Open-Source Tools (Sky130)

## 📝 Introduction

This repository contains my notes and documentation from a 5-day workshop on Digital VLSI Physical Design using open-source tools. This hands-on workshop covered the complete flow from RTL to GDSII using tools like Yosys, OpenLane, Magic, and the Sky130 PDK.


---

## 📅 Day 1: Inception of Open-Source EDA, OpenLANE and Sky130 PDK

- [🔸 How to talk to computers](#-how-to-talk-to-computers)
  - [Introduction to QFN-48 Package, chip, pads, core, die and IPs](#introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
  - [Introduction to RISC-V](#introduction-to-risc-v)
  - [From Software Applications to Hardware](#from-software-applications-to-hardware)

- [🔸 SoC Design and OpenLANE](#-soc-design-and-openlane)
  - [Introduction to all components of open-source digital ASIC design](#introduction-to-all-components-of-open-source-digital-asic-design)
  - [Simplified RTL2GDS flow](#simplified-rtl2gds-flow)
  - [Introduction to OpenLANE and Strive chipsets](#introduction-to-openlane-and-strive-chipsets)
  - [Introduction to OpenLANE detailed ASIC design flow](#introduction-to-openlane-detailed-asic-design-flow)

- [🔸 Get familiar with Open-Source EDA Tools](#-get-familiar-with-open-source-eda-tools)
  - [OpenLANE Directory structure in detail](#openlane-directory-structure-in-detail)
  - [Design Preparation Step](#design-preparation-step)
  - [Review files after design prep and run synthesis](#review-files-after-design-prep-and-run-synthesis)
  - [OpenLANE Project Git Link Description](#openlane-project-git-link-description)
  - [Steps to characterize synthesis results](#steps-to-characterize-synthesis-results)

---

## 📅 Day 2: Good Floorplanning Considerations

- 🔸 [Chip Floorplanning Consideration](#chip-floorplanning-consideration)
- [Utilization factor and aspect ratio](#utilization-factor-and-aspect-ratio)
- [Concept of pre-placed cells](#concept-of-pre-placed-cells)
- [Decoupling capacitors](#decoupling-capacitors)
- [Power planning](#power-planning)
- [Pin placement and logical cell placement blockage](#pin-placement-and-logical-cell-placement-blockage)
- [Steps to run floorplan using OpenLANE](#steps-to-run-floorplan-using-openlane)
- [Review floorplan files and steps to view floorplan](#review-floorplan-files-and-steps-to-view-floorplan)
- [Review floorplan layout in Magic](#review-floorplan-layout-in-magic)

- 🔸 [Library Building and Placement](#library-building-and-placement)
- [Netlist binding and initial place design](#netlist-binding-and-initial-place-design)
- [Optimize placement using estimated wire-length and capacitance](#optimize-placement-using-estimated-wire-length-and-capacitance)
- [Final placement optimization](#final-placement-optimization)
- [Need for libraries and characterization](#need-for-libraries-and-characterization)
- [Congestion aware placement using RePlAce](#congestion-aware-placement-using-replace)

- 🔸 [Cell Design and Characterization Flows](#cell-design-and-characterization-flows)
- [Inputs for cell design flow](#inputs-for-cell-design-flow)
- [Circuit design steps](#circuit-design-steps)
- [Layout design step](#layout-design-step)
- [Typical characterization flow](#typical-characterization-flow)

- 🔸 [General Timing Characterization Parameters](#general-timing-characterization-parameters)
- [Timing threshold definitions](#timing-threshold-definitions)
- [Propagation delay and transition time](#propagation-delay-and-transition-time)

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

### Introduction to QFN-48 Package, Chip, Pads, Core, Die, and IPs

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

###  Introduction to RISC-V

**RISC-V** (pronounced “risk-five”) is an open and free-to-use Instruction Set Architecture (ISA) that originated at the **University of California, Berkeley**. The “V” in RISC-V stands for the **fifth generation** of RISC design.

It is gaining popularity due to several advantages:
- ✅ Completely open-source — no licensing costs
- ✅ Modular — supports custom extensions
- ✅ Scalable — available in 32-bit, 64-bit, and even experimental 128-bit versions
- ✅ Backed by both academia and industry

Physically, the **die** inside a chip is connected to the external pins using **bond wires**. These wires serve as bridges between the internal circuits and the outside world.

<img width="721" height="401" alt="Screenshot 2025-07-17 144900" src="https://github.com/user-attachments/assets/bb78d8a2-b800-4555-8664-68cf636af731" />


---

###  From Software Applications to Hardware

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

#### Introduction to all components of open-source digital asic design


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

###  Simplified RTL2GDS flow

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

###  Introduction to OpenLANE and striVe Chipsets

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

###  Introduction to OpenLANE Detailed ASIC Design Flow

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

####  OpenLANE Directory structure in detail

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

###  Design Preparation Step

In OpenLANE, we use the `flow.tcl` script. Running with `-interactive` allows step-by-step execution.

<img width="954" height="925" alt="Screenshot 2025-07-17 152021" src="https://github.com/user-attachments/assets/0e81fc19-d1a5-4b23-886b-9c9a940e565a" />



Once inside the OpenLANE environment, the flow is controlled using the `flow.tcl` script. This script automates the entire ASIC design process. By using the `-interactive` switch, we can perform each stage manually, allowing more control and understanding. Without the `-interactive` switch, OpenLANE will execute the complete RTL to GDSII flow in one go.

Once OpenLANE is launched interactively, the prompt changes to indicate that we are now inside the OpenLANE shell.



Next, we load all the required packages necessary to run the OpenLANE flow.

<img width="954" height="1013" alt="Screenshot 2025-07-17 152024" src="https://github.com/user-attachments/assets/d06ccbd6-6749-497e-87a6-58c8438dcdbd" />

Now we are ready to execute our first command.

---

### Review files after design prep and run synthesis

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

###  Steps to Characterize Synthesis Results

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

## 📅 Day 2: Good Floorplanning Considerations

### Chip Floorplanning Consideration

During chip design, floorplanning is a critical step that defines how various blocks (standard cells, macros, IOs) are arranged within the chip die. A good floorplan minimizes area, reduces delay, and avoids routing congestion.
<img width="889" height="491" alt="Screenshot 2025-07-17 193615" src="https://github.com/user-attachments/assets/283c7f85-7b92-4f63-bcf3-95f96b7abf76" />


#### Utilization Factor and Aspect Ratio

- **Utilization Factor** determines how efficiently the available core area is used.
  <img width="249" height="212" alt="Screenshot 2025-07-17 193633" src="https://github.com/user-attachments/assets/8c967b4c-8047-423a-9498-8c5016dba176" />
  
<img width="349" height="307" alt="Screenshot 2025-07-17 193651" src="https://github.com/user-attachments/assets/3b76d3e3-0d9c-4093-850f-848cc60eeffb" />

  
  Utilization Factor = Area of Standard Cells/Core Area
  
<img width="528" height="309" alt="Screenshot 2025-07-17 193727" src="https://github.com/user-attachments/assets/fd51c0c6-61aa-435c-bd9f-ef677165a48f" />

  - A **high utilization factor** can lead to **routing congestion** due to lack of space for interconnects.
  - A **low utilization factor** wastes silicon area, increasing chip cost.

- **Aspect Ratio** is the ratio of height to width of the die or core area. An ideal aspect ratio is **close to 1**, which helps in achieving uniform routing and optimal performance.
<img width="889" height="502" alt="Screenshot 2025-07-17 193846" src="https://github.com/user-attachments/assets/0e4a3fa9-7e77-4f51-b269-85428a764fbc" />

---

### Concept of Pre-Placed Cells

<img width="890" height="496" alt="Screenshot 2025-07-17 193901" src="https://github.com/user-attachments/assets/54de3df8-cec6-4aa7-ad70-cd06350fdb5d" />

Before the standard cells are placed, certain elements must be **pre-placed** in the design:

- **IO Pins**: Placed along the periphery to interface with external components.
- **Macros**: Large functional blocks like memory, PLLs, etc.
- **Power Switches**: Control power gating and distribution.

These components are placed first to reserve fixed areas and guide the standard cell placement later.
<img width="887" height="505" alt="Screenshot 2025-07-17 193913" src="https://github.com/user-attachments/assets/3756cf26-1edc-4006-b856-8e3382a200e6" />

---

###  Decoupling Capacitors

When digital gates (like an AND gate) switch states — from `0` to `1` or `1` to `0` — a brief surge in current (known as **switching current**) is required to charge or discharge the internal capacitances.

Let’s assume there's an ideal switching capacitor with capacitance = 0.

During these transitions, due to the **resistance (Rdd)** and **inductance (Ldd)** in the power supply path, a **voltage drop** occurs. This causes the actual supply voltage at the switching node (Node A) to dip from the ideal Vdd to a slightly lower value, say Vdd′ (e.g., from `1V` to `0.97V`). 
<img width="634" height="393" alt="Screenshot 2025-07-17 193943" src="https://github.com/user-attachments/assets/297ce893-7976-436c-9052-0b920ae7e549" />


#### 🔍 Why This Is Dangerous:
- Logic `'1'` might now be interpreted as less than `1V` (e.g., `0.97V`)
- It may not satisfy **Noise Margin High (NMH)**
- Can lead to **incorrect logic evaluations** and unpredictable circuit behavior
  <img width="886" height="498" alt="Screenshot 2025-07-17 194007" src="https://github.com/user-attachments/assets/be32e5b1-220c-4843-834c-2386c578d2d4" />


#### 🛠 Solution:
To counter this, **Decoupling Capacitors (Cd)** are added **in parallel** with the switching circuit:
- When the logic gate switches, it **draws current from the decoupling capacitor** instead of the main supply
- The **resistor-inductor (RL) network** slowly recharges the capacitor
- This **maintains voltage stability** at the gate during rapid switching
<img width="675" height="418" alt="Screenshot 2025-07-17 194028" src="https://github.com/user-attachments/assets/1171bb05-90a9-4603-ac80-5c0a0124413c" />

#### 📌 In Real Chips:
- Decoupling capacitors are **strategically placed between functional blocks** (e.g., Block A, Block B, Block C)
- This ensures **localized and stable power delivery**
- Prevents logic errors due to sudden voltage dips
<img width="676" height="465" alt="Screenshot 2025-07-17 194042" src="https://github.com/user-attachments/assets/0ea65c3b-33af-4f12-9649-783c4eb511f9" />

---

###  Power Planning

Let's now treat the local circuit blocks as **black boxes** that are repeated across the chip. For proper functionality, **signals (0s and 1s)** must move reliably from drivers to loads.

However, if the **power source is far away**, issues can arise.

#### 🧠 Example:
Consider a **16-bit bus** connected to inverters:
- When all lines toggle, internal capacitors charge or discharge
- Discharging through a **single ground connection** creates **Ground Bounce**
- Charging through a **single Vdd tap** causes a **Vdd Drop**
<img width="760" height="488" alt="Screenshot 2025-07-17 194106" src="https://github.com/user-attachments/assets/e2ac46de-4236-4a4a-b21b-964c7c487cc5" />

---
<img width="883" height="484" alt="Screenshot 2025-07-17 194123" src="https://github.com/user-attachments/assets/3b120742-0a5a-4483-a8fc-75c5931aa130" />

#### ⚠️ Problem 1: Ground Bounce
- All capacitors discharging at once → bump in the ground rail
- If this bump **exceeds noise margin**, signals enter an undefined state
- May cause **incorrect values to be latched**
<img width="866" height="486" alt="Screenshot 2025-07-17 194137" src="https://github.com/user-attachments/assets/db8b9215-5ee7-46bb-ac06-9d0bbaec39a1" />

---

#### ⚠️ Problem 2: Vdd Drop
- Many capacitors charging at once from a single Vdd tap → voltage drop
- If Vdd dips below NMH → possible logic failure
<img width="863" height="477" alt="Screenshot 2025-07-17 194151" src="https://github.com/user-attachments/assets/bb11d0e7-e297-4639-a233-d99e616c031d" />

---

#### ✅ Solution: Power Mesh
The solution is to **distribute power uniformly** using a **Power Mesh**:
- Supply and ground taps are spread throughout the chip
- Each block draws power from its **nearest available source**
- Reduces stress on individual taps
- **Prevents excessive voltage dips and ground bounce**

<img width="782" height="493" alt="Screenshot 2025-07-17 194208" src="https://github.com/user-attachments/assets/d039259e-7264-4daa-bf99-0d9d2ba66de1" />
<img width="892" height="500" alt="Screenshot 2025-07-17 194226" src="https://github.com/user-attachments/assets/62f0d3e3-3598-42e7-8284-96208a239ca9" />


---

##  Pin Placement and Logical Cell Placement Blockage

Let's take a basic design scenario:

Two circuits are driven by different clocks (`clk1`, `clk2`), and take in data inputs (`Din1`, `Din2`) to produce outputs (`Dout1`, `Dout2`). Additionally:

- `BlockA` receives `Din1` and `Din2`
- `BlockB` takes both clocks and outputs `ClkOut`
<img width="741" height="398" alt="Screenshot 2025-07-17 194256" src="https://github.com/user-attachments/assets/c54fd4ae-3fb2-45c2-b486-376af3eff076" />

### 🧾 Total:
- Inputs: `clk1`, `clk2`, `Din1`, `Din2`
- Outputs: `Dout1`, `Dout2`, `ClkOut`

We can further increase complexity by adding logic across clock domains, potentially ending with **6 input and 5 output ports**.
<img width="560" height="491" alt="Screenshot 2025-07-17 194319" src="https://github.com/user-attachments/assets/bb4d030e-3255-484c-a720-fbe41488665f" />

---

## 🧠 What is a Netlist?

A **Netlist** is the **connectivity description** of a circuit, typically written in Verilog or VHDL. 

- The **frontend team** defines the netlist
- The **backend team** uses it for **layout, placement, and routing**

---

## 🧩 Pin & Block Placement Guidelines

- The **netlist** is placed inside the **core area** of the chip
- The space between **core and die edge** is used for **pin placement**
- Inputs to blocks should be **placed close** to minimize wire length and delay
<img width="671" height="496" alt="Screenshot 2025-07-17 194341" src="https://github.com/user-attachments/assets/6bbe320a-5b57-4804-ad17-64d17f4290cf" />

### ⏱ Clock Pin Placement:
- Clock pins are **larger than data pins**
- Reason: Clocks switch continuously and need **low-resistance paths**
- Wider clock pins → **lower resistance** → **better signal integrity**

---

## 🚫 Logical Cell Placement Blockage

Pin placement areas must be kept **free from standard logic cells** to:
- Avoid **routing congestion**
- Maintain **clean power paths**
- Ensure **signal integrity**

These reserved regions are called **Logical Cell Placement Blockages**.

- Clearly marked in layout tools
- Ensure there are **no cells placed** in pin zones to avoid interference

<img width="725" height="486" alt="Screenshot 2025-07-17 194400" src="https://github.com/user-attachments/assets/556e7219-5a1f-4d07-ab8b-bf2475c00fe6" />

---

##  Floorplanning in OpenLANE

###  Steps to Run Floorplan using OpenLANE

Before running the floorplanning stage in OpenLANE, certain configuration switches must be set. These parameters help guide how the chip layout is planned.

These switches can be found in various OpenLANE configuration files and control important aspects like chip area usage, pin placement, and power distribution.
<img width="952" height="1017" alt="Screenshot 2025-07-17 194802" src="https://github.com/user-attachments/assets/c5b632b9-3c48-4398-96a3-a0ddf851defe" />

From the image above, you can observe:

- **Core Utilization Ratio** is set to `50%` by default — this defines how much of the chip area is allowed to be used by standard cells.
- **Aspect Ratio** is set to `1` — which means the chip layout will be square by default.

These are just default values — we can (and often should) change them according to our design requirements.

Another important switch is `FP_PDN`, which deals with **Power Distribution Network (PDN)** settings. PDN setup is enabled by default during the floorplanning stage in OpenLANE.

Also, `FP_IO_MODE` values:
- `1` or `0` indicate pin placement is random, but the pins are spaced equally across the periphery.

---

### 🧩 Priority of Configuration Files

OpenLANE uses configuration files in the following order of priority (from **lowest** to **highest**):

1. `floorplan.tcl` → (Default system settings)  
2. `config.tcl` → (User-defined design config)  
3. `sky130A_sky130_fd_sc_hd_config.tcl` → (PDK variant-specific settings)
<img width="961" height="1014" alt="Screenshot 2025-07-17 194906" src="https://github.com/user-attachments/assets/7ed7de51-5d79-45d5-b8bc-70a06d8320bc" />

---

### Review floorplan files and steps to view floorplan

Once the floorplan is generated, you can inspect the configuration and layout using the files in the run folder:

- Open `config.tcl` to see which parameters were actually used in the flow.
  - This includes core utilization, aspect ratio, PDN settings, pin modes, etc.
<img width="957" height="1019" alt="Screenshot 2025-07-17 195019" src="https://github.com/user-attachments/assets/ed9d6193-eac7-4a69-ac20-4a8c8598dfca" />



To view the physical floorplan, navigate to:

```bash
results/floorplan/
```

In this folder, you’ll find a `.def` file (**Design Exchange Format**) which contains detailed layout data like die area, pin locations, and units.
<img width="955" height="1018" alt="Screenshot 2025-07-17 195623" src="https://github.com/user-attachments/assets/92afdb9b-1982-4991-a665-b360d649912f" />

Example values from `.def` file:

```scss
DIEAREA ( 0 0 ) ( 660685 671405 );
UNITS DISTANCE MICRONS 1000 ;
```

This means:
- Coordinates are in database units, where **1000 units = 1 micron**
- Width = `660685 / 1000 = 660.685 µm`
- Height = `671405 / 1000 = 671.405 µm`

---

### 🪄 View Floorplan in Magic

To visualize the layout, launch Magic using the following command:

```bash
magic -T /Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech \
lef read ../../tmp/merged.lef \
def read picorv32a.floorplan.def
```

Once you hit Enter, the Magic layout viewer will open and display the floorplan.
<img width="953" height="1027" alt="Screenshot 2025-07-17 195852" src="https://github.com/user-attachments/assets/2fc7d6d4-de77-4b3e-b501-db7affa2ec9c" />

---

###  Review Floorplan Layout in Magic

In the layout:
- Input/Output pins are placed at equal distances
- You can select objects by clicking on them and pressing `'s'` (highlight)
- To zoom in, press `'z'`, and to zoom out, press `Shift + z`
<img width="957" height="1016" alt="Screenshot 2025-07-17 195952" src="https://github.com/user-attachments/assets/a4770681-63c5-4434-8129-9d49225f6ca7" />


Once a pin is selected, you can use the `tkcon` window and type:

```tcl
what
```
<img width="955" height="1011" alt="Screenshot 2025-07-17 200113" src="https://github.com/user-attachments/assets/ebf5c15c-3307-4382-9b37-eadb8b3e2e34" />

This shows the **layer** and **position** details of the selected object.

For example:
- Horizontal pins might appear on **Metal 3**
- Vertical pins might be placed on **Metal 2**

---

### 🧱 Standard Cells and Decap Cells

You can also notice:
- **Decap Cells** are placed at the borders of the layout to stabilize voltage levels
- **Standard cells** like buffer 1, buffer 2, and AND gates are placed along rows

<img width="961" height="1014" alt="Screenshot 2025-07-17 200327" src="https://github.com/user-attachments/assets/613249d3-8231-44a4-8ab9-ceae1773b205" />

These observations are crucial for understanding the **structure** and **efficiency** of your chip design.



---
###  Library Building and Placement

---

####  Netlist Binding and Initial Place Design

**Binding Netlist with Physical Cells:**

- A netlist contains gates like NOT, AND, Flip-Flops, etc.
- In the physical world, these are represented as rectangular boxes with actual width and height.
- For each component, specific dimensions are assigned.
- These standard shapes (squares/rectangles) allow placement on silicon even though symbolic shapes (e.g., triangle for NOT) are used for functional clarity.
<img width="884" height="496" alt="Screenshot 2025-07-17 200718" src="https://github.com/user-attachments/assets/579f85da-64bc-4067-a2a8-4fd113b078d7" />

📚 **Library** is a shelf of all these logic elements (gates, flip-flops) and also includes:
- Timing information (delay, drive strength, etc.)
- Variants of cells (e.g., bigger versions with lower resistance = faster operation)
<img width="890" height="498" alt="Screenshot 2025-07-17 200729" src="https://github.com/user-attachments/assets/128e85fc-768c-4b1f-8886-6c6bbfa80626" />

---

##  Placement

- Once size and shape are defined, components from the netlist are placed on the **floorplan**.
- The floorplan includes IO ports and area.
- Placement ensures:
  - Logical connectivity is respected.
  - Timing paths are minimized.
  - No overlap with pre-placed macros.
<img width="897" height="503" alt="Screenshot 2025-07-17 200742" src="https://github.com/user-attachments/assets/13369837-ab1a-4482-96d9-c812c91f510a" />
<img width="884" height="506" alt="Screenshot 2025-07-17 200756" src="https://github.com/user-attachments/assets/635a8dd4-1a39-4fdc-8f9a-1cda61b5afd1" />
<img width="887" height="484" alt="Screenshot 2025-07-17 201051" src="https://github.com/user-attachments/assets/00127755-61d8-4a15-8a0a-20ba6f782849" />

---

## Optimize placement using estimated wire-length and capacitance

<img width="889" height="493" alt="Screenshot 2025-07-17 201119" src="https://github.com/user-attachments/assets/74db9b52-b551-4a65-b649-1fbbf562d9b5" />

- **Problem**: FF1 and Din2 are far apart → large wire → high resistance/capacitance → delay.
- **Solution**: Insert repeaters (buffers) between long wires to maintain signal integrity.
<img width="900" height="497" alt="Screenshot 2025-07-17 201147" src="https://github.com/user-attachments/assets/ec47ae4f-016f-4d3d-9efb-8d4a0aa63816" />

📘 **Repeaters**:
- Re-generate original signals.
- Used when wire length is too long for a single driver.

**Trade-off**: Improved signal integrity vs. increased area usage.

---

##  Final Placement Optimization

- Similar to Stage 2, Stage 3 may also require buffers.
<img width="889" height="490" alt="Screenshot 2025-07-17 201210" src="https://github.com/user-attachments/assets/8c007771-6f90-46e6-a896-1318cfc16a70" />

  
- **Stage 4** involves **Timing Analysis**:
  - Checks whether signal paths meet setup/hold time.
  - Uses ideal clocks for initial verification.
<img width="896" height="496" alt="Screenshot 2025-07-17 201229" src="https://github.com/user-attachments/assets/f7151dde-bd67-4069-a281-8d6f77876d23" />

---

##  Need for Libraries and Characterization

Each step of the IC design flow requires accurate library information.

### IC Design Flow Steps:
1. **Logic Synthesis**: RTL → Gate-level netlist.
2. **Floorplanning**: Define core/die size.
3. **Placement**: Assign physical locations.
4. **CTS**: Deliver clock evenly.
5. **Routing**: Wire-level connectivity.
6. **STA**: Check timing, frequency, setup/hold violations.

🔁 Common factor: **Standard cells** from library used across all steps.

---

##  Congestion Aware Placement using RePlAce

- **Objective**: Reduce congestion, not timing.
- **Two stages**:
  - Global Placement (no legalization)
  - Detailed Placement (legalization happens)

  
<img width="954" height="1016" alt="Screenshot 2025-07-17 201526" src="https://github.com/user-attachments/assets/66a037b6-2450-4b4a-be10-301bb3305614" />

🔍 View in **Magic**:
- Standard cells visible (gates, FFs, buffers).
<img width="955" height="1017" alt="Screenshot 2025-07-17 201608" src="https://github.com/user-attachments/assets/b1e29824-d48c-4ef3-ba24-e1d3725e245c" />

---

##  Cell Design and Characterization Flows

---
<img width="884" height="479" alt="Screenshot 2025-07-17 201840" src="https://github.com/user-attachments/assets/b96ed6fc-8b32-42f9-b18b-d7a6dfff5614" />

###  Inputs for Cell Design Flow

- PDKs, DRC/LVS rules, SPICE models, user-defined specs.
- DRC & LVS via `.tech` file.
- SPICE defines transistor behavior.
<img width="888" height="485" alt="Screenshot 2025-07-17 201857" src="https://github.com/user-attachments/assets/21fcd500-d41a-46fa-be75-4b641e7469ea" />

---

###  Circuit Design Steps

1. Implement function using PMOS/NMOS.
2. Ensure compatibility with library constraints (e.g., drive strength, size).
3. Generate CDL (Circuit Description Language), GDSII, LEF, Extracted SPICE Netlist (.cir).
<img width="874" height="496" alt="Screenshot 2025-07-17 201952" src="https://github.com/user-attachments/assets/9c497bea-c645-4369-8c6b-2de15960ecd3" />

---

###  Layout Design Step

1. Implement circuit using transistors.
2. Generate **network graphs**.
<img width="915" height="497" alt="Screenshot 2025-07-17 202026" src="https://github.com/user-attachments/assets/cf56d21a-989b-48bc-ac82-9e89a213b81b" />

3. Find **Euler’s path** → ensures efficient layout.
  <img width="891" height="487" alt="Screenshot 2025-07-17 202053" src="https://github.com/user-attachments/assets/9b06db78-2e5d-4e86-b66c-d21f16319bff" />

4. Draw **stick diagram**.
   <img width="492" height="301" alt="Screenshot 2025-07-17 202133" src="https://github.com/user-attachments/assets/a053a32a-0e84-4988-83be-503241ee9e12" />

5. Convert to **physical layout**.
    <img width="282" height="321" alt="Screenshot 2025-07-17 202211" src="https://github.com/user-attachments/assets/9dc58bf5-d6d4-48b0-9302-b139d44d324c" />

6. Extract parasitics and prepare for timing characterization.

---

##  Typical Characterization Flow

1. Read model and netlist.
2. Define buffer behavior.
3. Attach power supplies.
4. Apply input stimulus.
5. Add output capacitance.
   <img width="762" height="420" alt="Screenshot 2025-07-17 202238" src="https://github.com/user-attachments/assets/28d51fb3-6f1f-48d2-b75a-d6eb50938aaf" />

6. Run simulations (`.tran`, `.dc`).
7. Feed all into config file for **GUNA** (characterization software).
<img width="883" height="501" alt="Screenshot 2025-07-17 202319" src="https://github.com/user-attachments/assets/d20bb71b-5409-4423-8154-457e79280288" />


🧾 Output: Power, Noise, Timing models.

---

## General Timing Characterization Parameters

###  Timing Threshold Definitions

**Slew thresholds** (typical values):
- `slew_low_rise_thr` → 20%
  <img width="880" height="486" alt="Screenshot 2025-07-17 202352" src="https://github.com/user-attachments/assets/32825336-11e4-445a-91e5-0f522d6984e1" />

- `slew_high_rise_thr` → 80%
  <img width="886" height="503" alt="Screenshot 2025-07-17 202410" src="https://github.com/user-attachments/assets/f5a6dca3-2c86-429a-95a5-23c55120a0db" />

- `slew_low_fall_thr` → 20%
<img width="887" height="502" alt="Screenshot 2025-07-17 202453" src="https://github.com/user-attachments/assets/623fcbf1-6019-40eb-b8cc-5a4d33ec3e3b" />

- `slew_high_fall_thr` → 80%
<img width="887" height="501" alt="Screenshot 2025-07-17 202509" src="https://github.com/user-attachments/assets/33bd2f76-15e0-4705-bc1b-18eec46ee381" />


**Delay thresholds** (typically 50%):
- `in_rise_thr`, `in_fall_thr`
<img width="873" height="486" alt="Screenshot 2025-07-17 202535" src="https://github.com/user-attachments/assets/255e53bf-2913-4b74-8a15-e17a209fc5d1" />

- `out_rise_thr`, `out_fall_thr`
<img width="887" height="504" alt="Screenshot 2025-07-17 202613" src="https://github.com/user-attachments/assets/07f3ab1e-7b3b-4b56-9308-b6affe79b56b" />

---

###  Propagation Delay and Transition Time

- **Delay** = `time(out_thr) - time(in_thr)`
- **Transition time (slew)** = `time(high_thr) - time(low_thr)`
<img width="890" height="496" alt="Screenshot 2025-07-17 202624" src="https://github.com/user-attachments/assets/60aefc28-717d-4369-9b9c-a6bb960e3b0e" />

🛑 **Important**:
- Poor choice of threshold → negative delay (invalid)
- Even with correct threshold, output arriving before input = negative delay
<img width="882" height="497" alt="Screenshot 2025-07-17 202636" src="https://github.com/user-attachments/assets/83c055a9-1377-43e1-9c01-b15984ad7a18" />



✅ Slew and delay values are essential for accurate STA and simulation. 

<img width="848" height="437" alt="Screenshot 2025-07-17 202733" src="https://github.com/user-attachments/assets/5dda03ae-23cb-46cf-b85b-6cb2b92b9d90" />
<img width="803" height="413" alt="Screenshot 2025-07-17 202749" src="https://github.com/user-attachments/assets/de8b95b8-54c2-41d9-a407-3b0869ed5ad5" />


---
