# 🚀 DIGITAL VLSI SOC DESIGN AND PLANNING  

## 📝 Introduction

This repository contains my notes and documentation from a 5-day workshop on Digital VLSI Physical Design using open-source tools. This hands-on workshop covered the complete flow from RTL to GDSII using tools like Yosys, OpenLane, Magic, and the Sky130 PDK.

---

## [Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK](#day-1---inception-of-open-source-eda-openlane-and-sky130-pdk)
* [How to talk to computers](#how-to-talk-to-computers)
  * [Introduction to QFN-48 Package, chip, pads, core, die and IPs](#introduction-to-qfn-48-package-chip-pads-core-die-and-ips)
  * [Introduction to RISC-V](#introduction-to-risc-v)
  * [From Software Applications to Hardware](#from-software-applications-to-hardware)
* [Soc design and OpenLANE](#soc-design-and-openlane)
  * [Introduction to all components of open-source digital asic design](#introduction-to-all-components-of-open-source-digital-asic-design)
  * [Simplified RTL2GDS flow](#simplified-rtl2gds-flow)
  * [Introduction to OpenLANE and Strive chipsets](#introduction-to-openlane-and-strive-chipsets)
  * [Introduction to OpenLANE detailed ASIC design flow](#introduction-to-openlane-detailed-asic-design-flow)
* [Get familiar to open-source EDA tools](#get-familiar-to-open-source-eda-tools)
  * [OpenLANE Directory structure in detail](#openlane-directory-structure-in-detail)
  * [Design Preparation Step](#design-preparation-step)
  * [Review files after design prep and run synthesis](#review-files-after-design-prep-and-run-synthesis)
  * [OpenLANE Project Git Link Description](#openlane-project-git-link-description)
  * [Steps to characterize synthesis results](#steps-to-characterize-synthesis-results)


## [Day 2 - Good floor planning considerations](#day-2---good-floor-planning-considerations)
* [Chip Floor planning consideration](#chip-floor-planning-consideration)
  * [Utilization factor and aspect ratio](#utilization-factor-and-aspect-ratio)
  * [Concept of pre-placed cells](#concept-of-pre-placed-cells)
  * [De-coupling capacitors](#de-coupling-capacitors)
  * [Power planning](#power-planning)
  * [Pin placement and logical cell placement blockage](#pin-placement-and-logical-cell-placement-blockage)
  * [Steps to run floorplan using OpenLANE](#steps-to-run-floorplan-using-openlane)
  * [Review floorplan files and steps to view floorplan](#review-floorplan-files-and-steps-to-view-floorplan)
  * [Review floorplan layout in Magic](#review-floorplan-layout-in-magic)
* [Library building and Placement](#library-building-and-placement)
  * [Netlist binding and initial place design](#netlist-binding-and-initial-place-design)
  * [Optimize placement using estimated wire-length and capacitance](#optimize-placement-using-estimated-wire-length-and-capacitance)
  * [Final placement optimization](#final-placement-optimization)
  * [Need for libraries and characterization](#need-for-libraries-and-characterization)
  * [Congestion aware placement using RePlAce](#congestion-aware-placement-using-replace)
* [Cell design and characterization flows](#cell-design-and-characterization-flows)
  * [Inputs for cell design flow](#inputs-for-cell-design-flow)
  * [Circuit design steps](#circuit-design-steps)
  * [Layout design step](#layout-design-step)
  * [Typical characterization flow](#typical-characterization-flow)
* [General timing characterization parameters](#general-timing-characterization-parameters)
  * [Timing threshold definitions](#timing-threshold-definitions)
  * [Propagation delay and transition time](#propagation-delay-and-transition-time)


## [Day 3 - Design library cell using Magic Layout and ngspice characterization](#day-3---design-library-cell-using-magic-layout-and-ngspice-characterization)
* [Labs for CMOS inverter ngspice simulations](#labs-for-cmos-inverter-ngspice-simulations)
  * [IO placer revision](#io-placer-revision)
  * [SPICE deck creation for CMOS inverter](#spice-deck-creation-for-cmos-inverter)
  * [SPICE simulation lab for CMOS inverter](#spice-simulation-lab-for-cmos-inverter)
  * [Switching Threshold Vm](#switching-threshold-vm)
  * [Static and dynamic simulation of CMOS inverter](#static-and-dynamic-simulation-of-cmos-inverter)
  * [Lab steps to git clone vsdstdcelldesign](#lab-steps-to-git-clone-vsdstdcelldesign)
* [Inception of layout ̂A CMOS faabrication process](#inception-of-layout-a-cmos-faabrication-process)
  * [Create Active regions](#create-active-regions)
  * [Formation of N-well and P-well](#formation-of-n-well-and-p-well)
  * [Formation of gate terminal](#formation-of-gate-terminal)
  * [Lightly doped drain (LDD) formation](#lightly-doped-drain-ldd-formation)
  * [Source ÃÂ drain formation](#source-drain-formation)
  * [Local interconnect formation](#local-interconnect-formation)
  * [Higher level metal formation](#higher-level-metal-formation)
  * [Lab introduction to Sky130 basic layers layout and LEF using inverter](#lab-introduction-to-sky130-basic-layers-layout-and-lef-using-inverter)
  * [Lab steps to create std cell layout and extract spice netlist](#lab-steps-to-create-std-cell-layout-and-extract-spice-netlist)
* [Sky130 Tech File Labs](#sky130-tech-file-labs)
  * [Lab steps to create final SPICE deck using Sky130 tech](#lab-steps-to-create-final-spice-deck-using-sky130-tech)
  * [Lab steps to characterize inverter using sky130 model files](#lab-steps-to-characterize-inverter-using-sky130-model-files)
  * [Lab introduction to Magic tool options and DRC rules](#lab-introduction-to-magic-tool-options-and-drc-rules)
  * [Lab introduction to Sky130 pdk's and steps to download labs](#lab-introduction-to-sky130-pdks-and-steps-to-download-labs)
  * [Lab introduction to Magic and steps to load Sky130 tech-rules](#lab-introduction-to-magic-and-steps-to-load-sky130-tech-rules)
  * [Lab exercise to fix poly.9 error in Sky130 tech-file](#lab-exercise-to-fix-poly9-error-in-sky130-tech-file)
  * [Lab exercise to implement poly resistor spacing to diff and tap](#lab-exercise-to-implement-poly-resistor-spacing-to-diff-and-tap)
  * [Lab challenge exercise to describe DRC error as geometrical construct](#lab-challenge-exercise-to-describe-drc-error-as-geometrical-construct)
  * [Lab challenge to find missing or incorrect rules and fix them](#lab-challenge-to-find-missing-or-incorrect-rules-and-fix-them)


## [Day 4 - Pre-layout timing analysis and importance of good clock tree](#day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
* [Timing modeling using delay tables](#timing-modeling-using-delay-tables)
  * [Lab steps to convert grid info to track info](#lab-steps-to-convert-grid-info-to-track-info)
  * [Lab steps to convert magic layout to std cell LEF](#lab-steps-to-convert-magic-layout-to-std-cell-lef)
  * [Introduction to timing libs and steps to include new cell in synthesis](#introduction-to-timing-libs-and-steps-to-include-new-cell-in-synthesis)
  * [Introduction to delay tables](#introduction-to-delay-tables)
  * [Delay table usage Part 1](#delay-table-usage-part-1)
  * [Delay table usage Part 2](#delay-table-usage-part-2)
  * [Lab steps to configure synthesis settings to fix slack and include vsdinv](#lab-steps-to-configure-synthesis-settings-to-fix-slack-and-include-vsdinv)
* [Timing analysis with ideal clocks using openSTA](#timing-analysis-with-ideal-clocks-using-opensta)
  * [Setup timing analysis and introduction to flip-flop setup time](#setup-timing-analysis-and-introduction-to-flip-flop-setup-time)
  * [Introduction to clock jitter and uncertainty](#introduction-to-clock-jitter-and-uncertainty)
  * [Lab steps to configure OpenSTA for post-synth timing analysis](#lab-steps-to-configure-opensta-for-post-synth-timing-analysis)
  * [Lab steps to optimize synthesis to reduce setup violations](#lab-steps-to-optimize-synthesis-to-reduce-setup-violations)
  * [Lab steps to do basic timing ECO](#lab-steps-to-do-basic-timing-eco)
* [Clock tree synthesis TritonCTS and signal integrity](#clock-tree-synthesis-tritoncts-and-signal-integrity)
  * [Clock tree routing and buffering using H-Tree algorithm](#clock-tree-routing-and-buffering-using-h-tree-algorithm)
  * [Crosstalk and clock net shielding](#crosstalk-and-clock-net-shielding)
  * [Lab steps to run CTS using TritonCTS](#lab-steps-to-run-cts-using-tritoncts)
  * [Lab steps to verify CTS runs](#lab-steps-to-verify-cts-runs)
* [Timing analysis with real clock using openSTA](#timing-analysis-with-real-clock-using-opensta)
  * [Setup timing analysis using real clocks](#setup-timing-analysis-using-real-clocks)
  * [Hold timing analysis using real clocks](#hold-timing-analysis-using-real-clocks)
  * [Lab steps to analyze timing with real clocks using OpenSTA](#lab-steps-to-analyze-timing-with-real-clocks-using-opensta)
  * [Lab steps to execute OpenSTA with right timing libraries and CTS assignment](#lab-steps-to-execute-opensta-with-right-timing-libraries-and-cts-assignment)
  * [Lab steps to observe impact of bigger CTS buffers on setup and hold timing](#lab-steps-to-observe-impact-of-bigger-cts-buffers-on-setup-and-hold-timing)


## [Day 5 -Final step for RTL2GDS using tritinRoute and openSTA](#day-5-final-step-for-rtl2gds-using-tritinroute-and-opensta)
* [Routing and design rule check (DRC)](#routing-and-design-rule-check-drc)
  * [Introduction to Maze Routing ÃÂ LeeÃÂs algorithm](#introduction-to-maze-routing---lees-algorithm)
  * [LeeÃÂs Algorithm conclusion](#lees-algorithm-conclusion)
  * [Design Rule Check](#design-rule-check)
* [Power Distribution Network and routing](#power-distribution-network-and-routing)
  * [Lab steps to build power distribution network](#lab-steps-to-build-power-distribution-network)
  * [Lab steps from power straps to std cell power](#lab-steps-from-power-straps-to-std-cell-power)
  * [Basics of global and detail routing and configure TritonRoute](#basics-of-global-and-detail-routing-and-configure-tritonroute)
* [TritonRoute Features](#tritonroute-features)
  * [TritonRoute feature 1 - Honors pre-processed route guides](#tritonroute-feature-1-honors-pre-processed-route-guides)
  * [TritonRoute Feature2 & 3 - Inter-guide connectivity and intra- & inter-layer routing](#tritonroute-feature2--3-inter-guide-connectivity-and-intra--inter-layer-routing)
  * [TritonRoute method to handle connectivity](#tritonroute-method-to-handle-connectivity)
  * [Routing topology algorithm and final files list post-route](#routing-topology-algorithm-and-final-files-list-post-route)

* [References](#references)
* [Acknowledgement](#acknowledgement)
    
---

### Day 1 - Inception of open-source EDA, OpenLANE and sky130 PDK

#### How to talk to computers?

#### Introduction to QFN-48 Package, chip, pads, core, die and IPs

The Arduino board features a chip (microprocessor) at its core, which interacts with other components on the board. The comprehensive design process for this chip, from its initial abstract concept down to its physical fabrication, is encompassed by the RTL to GDSII flow.
An Arduino system comprises both a physical programmable circuit board, commonly known as a microcontroller, and its accompanying software, the Integrated Development Environment (IDE). The IDE runs on a computer, enabling users to write and upload code to the physical Arduino board.
![Arduino Microcontroller Board](https://github.com/user-attachments/assets/dd795cfb-2015-4caf-abca-de163ab82a82)


#### Chip Components

* **Pads:** These are the interface points used to send and receive electrical signals from the chip's interior.
* **Core:** This central area of the chip houses all the essential logic gates.
* **Die:** Representing the total size of the integrated circuit, it's typically found at the corner of the chip.

**Example: RISC-V SoC**
A RISC-V System-on-Chip (SoC) integrates various Intellectual Property (IP) blocks such as SRAM, SOC logic, Analog-to-Digital Converters (ADCs), Digital-to-Analog Converters (DACs), and Serial Peripheral Interface (SPI). These are often referred to as foundry IPs.
All semiconductor devices rely on foundries, facilities where chips are manufactured using specialized processes like deposition, lithography, and more.
<img width="725" height="400" alt="RISC-V SoC Components" src="https://github.com/user-attachments/assets/8bc9e7ed-f8c4-42e7-a495-fd4c0213e4a4" />


#### Introduction to RISC-V

RISC-V, where "five" denotes the fifth generation of RISC (Reduced Instruction Set Computer) architecture developed at the University of California, Berkeley, is an open-standard Instruction Set Architecture (ISA) rooted in established RISC principles.
Unlike most other ISA designs, RISC-V is freely available under open-source licenses, incurring no usage fees. A growing number of companies have introduced or announced RISC-V hardware products. Furthermore, open-source operating systems now offer RISC-V support, and the ISA is integrated into several widely used software toolchains.
This instruction set is engineered for broad applicability. Its base instructions maintain a fixed 32-bit length with natural alignment. The ISA also supports variable-length extensions, allowing instructions to consist of any number of 16-bit segments.
The specification defines variants for 32-bit and 64-bit address spaces. While a 128-bit flat address space variant is described as an extrapolation, its specification remains "not frozen" due to limited practical experience with such expansive memory systems.
Chips are typically connected to their packages using bond wires.
<img width="721" height="401" alt="RISC-V Architecture" src="https://github.com/user-attachments/assets/ae445c5a-4def-4ffa-94cd-c746d7a7e8ad" />


#### From Software Applications to Hardware

Understanding how applications execute on a system involves a layered process:
Application Software → System Software → Hardware Chip

Applications feed into a block of system software, which then translates the entire program into binary language. The system software itself is composed of several layers:

* **Operating System:** Manages low-level system functions, including input/output operations and memory allocation.
* **Compiler:** Takes higher-level language output from the operating system (e.g., C, C++, Java) and converts it into hardware-dependent instructions.
* **Assembler:** Translates these instructions from the compiler into their corresponding binary numbers.

This binary data is then sent to the hardware, which performs the requested function and generates the output.
Instructions serve as an abstract interface, bridging the gap between high-level languages (like C) and the underlying hardware.
<img width="886" height="495" alt="Software to Hardware Flowchart" src="https://github.com/user-attachments/assets/041abb2c-c465-459d-a1a4-9423d34ef8d8" />


#### Soc design and OpenLANE

#### Introduction to all components of open-source digital asic design

Designing a Digital ASIC requires several key elements from the outset: RTL Design, EDA Tools, and PDK Data.

**What is RTL Design?**
In digital circuit design, Register-Transfer Level (RTL) is an abstraction that models a synchronous digital circuit. It focuses on the flow of digital signals (data) between hardware registers, and the logical operations performed on those signals.
Numerous open-source resources for RTL designs are available on platforms like librecores.org, opencores.org, and github.com.

**What are EDA Tools?**
Electronic Design Automation (EDA) refers to the software tools used for designing and verifying Integrated Circuits (ICs), Printed Circuit Boards (PCBs), and electronic systems in general.
Notable open-source EDA tools include Qflow, OpenROAD, and OpenLANE.

**What is PDK Data?**
A Process Design Kit (PDK) acts as the interface between the fabrication (FAB) facility and the design team.
PDK data consists of various files, such as:

* Process design rules (e.g., DRC, LVS, REX)
* Digital standard cell libraries
* I/O libraries, etc.

These files model the fabrication process for EDA tools used in IC design. For instance, in 2020, Google released an open-source PDK for FOSS 130nm production based on SkyWater Technology. While cutting-edge technology now extends to 5nm, 130nm processors remain viable and cost-effective for many applications.

**Performance Example:** An Intel P4EE @3.46 GHz (Q4'04) can be compared to a Sky130_OSU (single cycle RV32i CPU) pipelined version, which can achieve over 1 GHz clock speeds.

#### Simplified RTL2GDS flow

<img width="891" height="497" alt="RTL2GDS Flow Diagram" src="https://github.com/user-attachments/assets/7a5bd5f6-bdc2-4899-a6ba-8cd99ede2ba2" />

**Step 1. Synthesis:**
Synthesis is the process where the Register-Transfer Level (RTL) design is translated into a gate-level netlist using a Standard Cell Library (SCL). This resulting circuit, described in Hardware Description Language (HDL), is functionally equivalent to the original RTL.
Standard Cells are pre-designed, regular layouts with defined electrical characteristics (e.g., described in HDL, SPICE models).

**Step 2. Floor/Power Planning:**
The primary goal is to organize the silicon area efficiently and ensure comprehensive power distribution throughout the circuit.
Chip floor planning involves partitioning the chip die into different system building blocks and placing the I/O pads.
Micro floor planning defines precise dimensions, pin locations, and row arrangements within these blocks.
Power planning constructs the power delivery network. Typically, the chip is supplied with power via multiple VDD (power) and GND (ground) connections. Components are then linked to the power supply using horizontal and vertical metal straps. Parallel structures are commonly employed to minimize resistance.
To mitigate electromigration issues, the power distribution network often utilizes thicker, upper metal layers, which offer lower resistance compared to thinner, lower layers.
<img width="452" height="203" alt="Power Network Example" src="https://github.com/user-attachments/assets/7d977f68-b9bf-40f4-8cf2-d89c65476d9d" /><img width="537" height="144" alt="Floorplanning" src="https://github.com/user-attachments/assets/63dbcad2-7ceb-4464-ac59-1b95867b14a6" />

**Step 3. Placement:**
In this stage, the gate-level netlist (representing the circuit's logic gates) is arranged onto the pre-defined floor planning rows, aligning with specific placement sites. Cells are positioned close to each other to minimize interconnect delay.
Placement typically involves two phases:

* **Global Placement:** This initial phase roughly positions cells within the core area, considering overall timing and congestion. Its aim is a coarse solution that might temporarily violate some placement constraints but provides a holistic view of the netlist.
* **Detailed Placement:** This subsequent phase refines the placement, determining the exact locations, routes, and layers for each net. The objectives are to achieve valid routing, minimize chip area, meet timing constraints, and reduce via count and power consumption.
<img width="530" height="201" alt="Placement Stages Diagram" src="https://github.com/user-attachments/assets/dc35f46a-ed1d-403f-a69a-a2383970036e" />


**Step 4. Clock Tree Synthesis (CTS):**
Before routing general signals, the clock signal must be routed. Clock Tree Synthesis distributes the clock signal to every sequential element, such as flip-flops, registers, ADCs, and DACs.
A clock network typically resembles a tree structure, with the clock source as the root and the sequential elements as the leaves.
CTS aims to synthesize this network to ensure minimal clock skew (the difference in arrival times of the clock signal to different elements) and an optimal clock shape. Low-skew global routing resources are utilized for clock signals to achieve this.
Microsemi devices, for instance, provide various global routing resources specifically designed to reduce skew. Common clock tree topologies include H-trees and X-trees.
<img width="169" height="134" alt="Clock Tree Synthesis Example" src="https://github.com/user-attachments/assets/8e05f214-382a-47ff-afbc-d0c50f0dab5a" />


**Step 5. Routing:**
Following clock routing, signal routing connects the remaining signal pins using various metal layers. Routing is the stage after CTS and optimization, where precise paths are determined for interconnections between standard cells, macros, and I/O pins.
In VLSI systems, two types of nets demand special attention during routing:

* Clock nets
* Power/Ground nets

The sky130 PDK specifies 6 routing layers. The innermost layer is the local interconnect layer (titanium nitride). The other five layers are made of aluminum.
Given the immense size of routing grids formed by metal tracks, a divide-and-conquer approach is employed for routing.
Two main types of routing are utilized:

* **Global routing:** Generates initial routing guides.
* **Detailed Routing:** Implements the actual physical wiring based on these routing guides.
<img width="506" height="194" alt="Routing Process Diagram" src="https://github.com/user-attachments/assets/25dc5dca-44aa-4a6c-b1bb-e367a077544e" />


**Step 6. Sign Off:**
Once routing is complete, the final layout is constructed. This layout then undergoes a thorough verification process.
Two primary types of verification are performed:

* **Physical Verification:** Involves Design Rule Checking (DRC) to ensure the final layout adheres to fabrication rules and matches the owner's layout specifications.
* **Timing Verification:** Conducts Static Timing Analysis (STA) to identify and report any timing violations present in the design.

#### Introduction to OpenLANE and Strive chipsets

OPENLANE is an automated RTL-to-GDSII flow that integrates various tools like OpenROAD, Yosys, Magic, Netgen, Fault, CVC SPEF-Extractor, CU-GR, and Klayout, along with numerous scripts for design exploration and optimization.
It originated as an open-source flow, designed for genuinely open-source tape-out experiments.
striVe represents a family of SoCs (System-on-Chips) that are "open everything": utilizing an Open PDK, Open EDA tools, and Open RTL.

**striVe SoC Family**
<img width="837" height="466" alt="striVe SoC Family Example" src="https://github.com/user-attachments/assets/26b534b0-5263-4a75-a73a-3d9c95ed9fe0" />

OPENLANE's core objective is to generate a flawless GDSII file with no human intervention (a "no-human-in-the-loop" approach). A "clean" GDSII implies:

* No Layout Versus Schematic (LVS) violations
* No Design Rule Check (DRC) violations
* No timing violations

OPENLANE is optimized for the SkyWater 130nm open PDK and can be used to harden both macros and complete chips.
It supports two operational modes:

* **Autonomous:** This "push-button" flow enables time-based design, culminating directly in the final GDSII.
* **Interactive:** This mode allows users to execute commands and steps sequentially, providing greater control.

The flow includes a comprehensive set of design examples (43 designs, each with its optimized configuration).

#### Introduction to OpenLANE detailed ASIC design flow
<img width="857" height="476" alt="OpenLANE Detailed ASIC Flowchart" src="https://github.com/user-attachments/assets/0c3a0fb6-6558-4940-b351-acf8a82d8c4b" />

The design exploration utility also supports regression testing (Continuous Integration - CI). OpenLANE is run on approximately 70 designs, and their results are benchmarked against known optimal configurations.

**DFT (Design for Test):** This stage incorporates scan insertion, automatic test pattern generation, test pattern compaction, fault coverage analysis, and fault simulation.
Subsequently, physical implementation is carried out by the OpenROAD application. This process involves several critical steps:

* Floor/Power Planning
* Insertion of End Decoupling Capacitors and Tap cells
* Placement (Global and Detailed)
* Post-Placement Optimization
* Clock Tree Synthesis (CTS)
* Routing (Global and Detailed)

The netlist is modified at various points (e.g., during CTS and Post-Placement Optimization), necessitating verification. Logical Equivalence Checking (LCE), typically using Yosys, formally confirms that the circuit's functionality remains unchanged after netlist modifications.

#### Dealing with antenna rules Violation

During fabrication, a metal wire segment can inadvertently act as an antenna, accumulating charges that may damage transistor gates.
<img width="411" height="206" alt="Antenna Effect Diagram" src="https://github.com/user-attachments/assets/28e1efac-2850-47ef-89d0-07c5aabbc718" />

To mitigate this, wire lengths must be limited, a task typically handled by the router. If the router fails, two solutions exist:

* **Bridging:** Attaching a higher-layer intermediary connection.
* **Adding antenna diode cells:** These cells, provided by the Standard Cell Library (SCL), are designed to safely discharge accumulated charges.
<img width="543" height="206" alt="Bridging and Antenna Diode Solutions" src="https://github.com/user-attachments/assets/6ccfe6da-1f3b-4b85-a0af-dcdb91e65df6" />

OpenLANE employs a preventive strategy: after placement, a "fake" antenna diode is added next to every cell input. An Antenna checker is then run on the routed layout. If a violation is reported on a cell input pin, the fake diode is replaced with a real one.
<img width="256" height="199" alt="OpenLANE Antenna Prevention Flow" src="https://github.com/user-attachments/assets/241917e3-bd36-4d29-b1b6-ef4b1c9ced3b" />

#### Static Timing analysis (STA)

This process involves extracting interconnect RC (Resistance-Capacitance) data (DEF2SPEF) from the routed layout, followed by Static Timing Analysis using the OpenSTA (OpenROAD) tool. The resulting report highlights any timing violations.

#### Physical Verification (DRC and LVS)

* Magic is utilized for Design Rules Checking (DRC) and SPICE extraction from the layout.
* Both Magic and Netgen are employed for Layout Versus Schematic (LVS) verification.

#### Get familiar to open-source EDA tools

#### OpenLANE Directory structure in detail

#### Basic Linux Commands

* `cd`: Change directory.
* `ls`: List directory contents.
* `pwd`: Print working directory.
* `mkdir`: Make a new directory.
* `command --help`: Display usage information for a command.
* `clear`: Clear the terminal screen.

We are currently working with the Sky130_fd_sc_hd PDK variant. In this name:

* "sky130" denotes the process name or technology node.
* "fd" indicates the foundry name (SkyWater Foundry).
* "sc" signifies standard cell library files.
* "hd" stands for high density, representing a specific variant.

The Sky130_fd_sc_hd variant includes various technology files such as Verilog, SPICE, techlef, meglef, mag, gds, cdl, lib, and lef. The techlef file specifically contains layer information.

#### Design Preparation Step

Upon entering the OpenLANE environment, the `flow.tcl` script is executed to guide the design flow. Using the interactive switch enables a step-by-step process, whereas omitting it would trigger a full RTL-to-GDSII run. Once OpenLANE starts, the terminal prompt changes.
<img width="954" height="925" alt="OpenLANE Interactive Prompt" src="https://github.com/user-attachments/assets/2dc1c75b-0b85-40c0-9735-141036544913" />

All necessary packages required for the flow must then be loaded.
<img width="954" height="1013" alt="OpenLANE Package Input Example" src="https://github.com/user-attachments/assets/a4090685-ed1d-4580-8500-38c8b1209b36" />

After package loading, commands are ready for execution.
Within the OpenLane design folder, approximately 30-40 pre-built designs are available. Any of these designs can be opened; for example, `picorv32a.v`. This design folder typically contains files like `src` and `config.tcl`. The `config.tcl` file stores detailed design parameters, including details about enrollment, clock period, and clock port.
<img width="955" height="1013" alt="config tcl Clock Period Setting" src="https://github.com/user-attachments/assets/3a9758f1-df8c-4fab-b32e-0557dc17e9a2" />


The screenshot shows the time period set to 5.00 nsec. However, if we examine the `openlane/sky130_fd_sc_hd` folder, the default period might be around 24 nsec. This indicates that the `config.tcl` in the design folder does not override the main library file; if an override were to occur, the main folder's settings would take precedence.

To prepare the design setup stage before running synthesis in OpenLane, the command is:

```bash
prep -design picorv32a
```
<img width="948" height="1012" alt="OpenLANE Prep Design Command Output " src="https://github.com/user-attachments/assets/61fd0d65-e25d-4132-aaeb-e252cd1d4a82" />


The output confirms that the preparation phase has been successfully completed.

#### Review files after design prep and run synthesis

Upon completion of the preparation phase, a unique run directory, named with the current date, is created within the `picorv32a` file structure. This directory contains essential folders for OpenLane operations.
The `tmp` folder within this run directory houses the `merged.lef` file, generated during preparation. Opening `merged.lef` reveals comprehensive wire, layer, and cell-level information.

<img width="961" height="1014" alt="Merged LEF File Content" src="https://github.com/user-attachments/assets/a6ebd8c7-6895-41d4-bed3-7c69c7687fe7" />


Initially, the `result` folder remains empty because no processing has occurred yet. The `report` folder, however, is populated with sub-folders designated for synthesis, placement, floorplanning, CTS, routing, Magic, and LVS reports.
Another `config.tcl` file exists within this run directory, mirroring the one in the design folder. This file captures all default parameters utilized for the current run. When modifications are made to the original configuration (e.g., changing core utilization in floorplanning) and the flow is re-run, this `config.tcl` updates to reflect those changes, allowing for cross-verification that modifications were effectively applied.

To proceed with synthesis in OpenLane, the command is:

```bash
run_synthesis
```
This synthesis process typically takes 3-4 minutes to complete.

<img width="956" height="1017" alt="OpenLANE Run Synthesis Command Output 1" src="https://github.com/user-attachments/assets/efe02b91-5cbc-4651-868f-df447510f10f" />
<img width="958" height="1013" alt="OpenLANE Run Synthesis Command Output 2" src="https://github.com/user-attachments/assets/f2f37dd4-d5ac-4060-a62b-bf2229e24bc6" />



#### Steps to characterize synthesis results

From the synthesis output data:

* The total count of D-flip-flops is 1613.
* The total number of cells is 14876.
<img width="953" height="1017" alt="Synthesis Results Table" src="https://github.com/user-attachments/assets/1fc829d7-5b83-4596-a2ca-6d4a8ca3426f" />


Therefore, the flop ratio (number of flip-flops / total number of cells) is 10.84%.
As observed before the run, the result folder was empty. However, after synthesis, it now shows that all mapping has been successfully performed by ABC.

<img width="953" height="1019" alt="Synthesis ABC Mapping Results" src="https://github.com/user-attachments/assets/6ab864d9-2982-4923-b877-a8e1ea36b407" />


The report indicates the actual time of synthesis completion, and the synthesis statistics report displayed below confirms the figures observed earlier.

<img width="961" height="1019" alt="Synthesis Statistics Report" src="https://github.com/user-attachments/assets/2531aa9e-ad12-41f0-a3ae-d536e6ff68c8" />

---

### Day 2 - Good floor planning considerations

#### Chip Floor planning consideration

#### Utilization factor and aspect ratio

This section focuses on determining the width and height of the chip's Core and Die, which is the initial step in the physical design flow.

Let's start with a simple netlist, consisting of two flip-flops interconnected by basic combinational logic. A netlist primarily describes the electronic design's connectivity. Our calculations will depend on the physical dimensions of the logic gates (like AND & OR) and the flip-flops involved. The goal is to convert these logical symbols into physical dimensions.

Our primary interest lies in the dimensions of the Core and Die, rather than the dimensions of the interconnecting wires.

Assume:
* A standard cell has dimensions of 1 unit x 1 unit, resulting in an area of 1 square unit.
* A flip-flop also occupies 1 square unit of area.

Using these assumed dimensions and the netlist, we can calculate the area the netlist would occupy on a silicon wafer.

<img width="889" height="491" alt="Screenshot 2025-07-17 193615" src="https://github.com/user-attachments/assets/499abbb7-2ec6-4871-8471-c84d26c3259e" />

To estimate the minimum area, we first conceptualize all wires as removed, consolidating all flip-flops and logic gates onto a single plane. After combining them, the total width and length become 2 units each.

This results in a total occupied area of 4 square units. This gives us a rough estimate of the minimum area required by the netlist.

<img width="249" height="212" alt="Screenshot 2025-07-17 193633" src="https://github.com/user-attachments/assets/7bfc4af9-edbf-42c5-862e-fed14a92f9e6" />

#### What is 'Core' and 'Die' section of a chip?

Imagine a silicon wafer where all the logic circuits are implemented. Within this wafer, a specific section is termed the 'Die', and inside the Die, we find the 'Core'.

A **Die** is a small semiconductor material specimen upon which the fundamental circuit is fabricated. It encompasses the core logic.
A **Core** is the designated section of the chip where the primary logical design of the circuit is placed.

<img width="349" height="307" alt="Screenshot 2025-07-17 193651" src="https://github.com/user-attachments/assets/733596e7-d1d7-41e4-8d45-dc4357d802f9" />

Now, let's attempt to place our calculated logic (netlist) inside the core. If the netlist occupies the entire core area, it implies a 100% core utilization. From this, we can calculate the Utilization Factor using the formula:

$$ Utilization~Factor = \frac{Area~occupied~by~netlist}{Total~area~of~the~core} $$

Given our dimensions (netlist area = 4 square units, core dimensions = 2 units x 2 units = 4 square units):

$$ Utilization~Factor = \frac{4~sq.~unit}{4~sq.~unit} = 1 $$

A utilization factor of 1 indicates that the core is 100% utilized, with no remaining space.

The Aspect Ratio is calculated as:

$$ Aspect~Ratio = \frac{Width}{Height} = \frac{2~unit}{2~unit} = 1 $$

An Aspect Ratio of 1 signifies a square-shaped chip. If the aspect ratio deviates from 1, the chip will be rectangular.

**Example:**
Let's consider different core dimensions: width = 4 units and height = 2 units.
Using the Utilization Factor formula, we get 0.5. This means the netlist only covers 50% of the core area, leaving space.
The Aspect Ratio would be 0.5, indicating a rectangular chip.
The leftover area within the core can be utilized for placing additional cells, such as buffers, or for routing purposes.
<img width="528" height="309" alt="Screenshot 2025-07-17 193727" src="https://github.com/user-attachments/assets/2aad818e-38ac-465d-917e-32d34b8abfae" />


#### Utilization factor and aspect ratio

Let's consider another example: a square chip with dimensions 4x4 square units.
In this scenario, the utilization factor would be 0.25. This means only 25% of the total chip area is utilized by the netlist, leaving 75% available. This available space can be used for additional cells or for routing, which often involves multiple metal layers.
The aspect ratio remains 1, confirming the chip's square shape.

<img width="889" height="502" alt="Screenshot 2025-07-17 193846" src="https://github.com/user-attachments/assets/4f2683fa-3427-4462-8868-2e5da22856d5" />

#### Define locations of Preplaced Cells

Consider a large combinational logic circuit performing a specific function, comprised of many logic gates. We can subdivide this large circuit into smaller, manageable blocks. For instance, we can partition the entire circuit into two distinct blocks, to be implemented separately.

<img width="890" height="496" alt="Screenshot 2025-07-17 193901" src="https://github.com/user-attachments/assets/b2ee54ec-5684-4426-bd3c-0abef9cb17f2" />

For both blocks, we can extend their input/output pins. Then, we "black-box" these blocks, effectively detaching them conceptually. Once black-boxed, their internal structure becomes invisible from a higher-level view (e.g., to someone examining the main netlist). These separated blocks can then function as independent IPs (Intellectual Properties) or modules.

<img width="887" height="505" alt="Screenshot 2025-07-17 193913" src="https://github.com/user-attachments/assets/97f0ea19-1289-4669-a6ba-b08a10313864" />

The primary advantage of this approach is reusability: once implemented, these blocks can be reused multiple times across different designs.

Similarly, other types of IPs like Memory, Clock-gating cells, Comparators, and MUXes are often part of a top-level netlist. They receive signals, perform their specific functions, and deliver outputs, but their core functionality is implemented only once.

The strategic arrangement of these IPs within a chip is referred to as floorplanning.

These IPs, having user-defined locations, are placed on the chip before automated placement and routing. They are thus termed "pre-placed cells".

Their placement is meticulously planned to ensure that the automated placement and routing tools do not alter their designated locations.

#### De-coupling capacitors

To understand the role of Decoupling Capacitors, let's consider a specific circuit block mentioned earlier. When a gate, such as an AND gate, switches its state (from 0 to 1 or 1 to 0), it requires a certain amount of switching current due to the presence of small internal capacitances. This capacitance must be fully charged for a logic '1' and fully discharged for a logic '0'.

Assuming ideal conditions, where Rdd, Ldd (power supply resistance/inductance) and Lss (ground supply inductance) have defined values, during a switching operation, the circuit demands a peak current.

Due to the inherent resistance (Rdd) and inductance (Ldd) in the power supply path, there will be a voltage drop across them. Consequently, the voltage at an internal node (let's call it Node 'A') might be Vdd' instead of the ideal Vdd.

<img width="634" height="393" alt="Screenshot 2025-07-17 193943" src="https://github.com/user-attachments/assets/ea2424cc-89e1-4ad5-8963-7a8ebb0ab6a9" />

For example, if ideal logic '1' is 1 Volt, it might practically be less, say 0.97 Volts (Vdd'). This deviation can be critical if it falls within the undefined range of Noise Margins (NM low and NM high), posing a significant risk to circuit reliability.

<img width="886" height="498" alt="Screenshot 2025-07-17 194007" src="https://github.com/user-attachments/assets/7ec59b63-0846-4815-9a19-8820cb9ef366" />

To solve this problem, Decoupling Capacitors (Cd) are placed in parallel with the circuit. Whenever the circuit switches, it draws current directly from Cd. Meanwhile, the RL (resistor-inductor) network of the power supply path replenishes the charge into Cd. This ensures that Cd supplies the instantaneous current peaks demanded by the circuit.

<img width="675" height="418" alt="Screenshot 2025-07-17 194028" src="https://github.com/user-attachments/assets/64ef2a1b-a709-479e-afa5-a421ccbde3d5" />

In a chip, decoupling capacitors are typically positioned between various functional blocks (e.g., Block A, Block B, and Block C, as shown above). This strategic placement ensures that the local current demands of these blocks are effectively met by the decoupling capacitors, addressing local power fluctuations.

<img width="676" height="465" alt="Screenshot 2025-07-17 194042" src="https://github.com/user-attachments/assets/4bdefe89-f24e-43fc-87f0-b30b035dd6cd" />

#### Power planning

Let's consider a local circuitry block, which can be replicated multiple times and includes logic elements at its boundaries. While decoupling capacitors address local current demands within these blocks, the issue of power delivery to broader interconnects remains.

Imagine a signal transmitted from a driver to a load, typically switching from logic 0 to logic 1. It's crucial to maintain signal integrity along this path, ensuring the load receives the intended signal without degradation.

Now, consider a 16-bit bus that needs to maintain signal integrity from the driver to the load, requiring sufficient power from the supply. Unlike individual blocks, it's often not feasible to place decoupling capacitors across the entire bus length. If the main power supply is physically distant from the bus, a voltage drop will inevitably occur along the power lines.

<img width="760" height="488" alt="Screenshot 2025-07-17 194106" src="https://github.com/user-attachments/assets/4f42737d-61d1-46af-b236-eb20a1b8588a" />

When a particular line of the 16-bit bus transitions to logic 1, it means its associated capacitor is being charged to Vdd. Conversely, for logic 0, the capacitor is discharged to ground. If this 16-bit bus is connected to an inverter, all initially charged capacitors will discharge, and vice-versa.

<img width="883" height="484" alt="Screenshot 2025-07-17 194123" src="https://github.com/user-attachments/assets/0007cb32-d89c-4068-bc60-cc9d8d4597a9" />

A significant problem arises if all capacitors are connected to a single ground point. During discharge, this can cause a transient increase, or "bump," in the ground reference voltage at the common ground tap point. This phenomenon is known as Ground Bounce. If the magnitude of this bounce exceeds the noise margin, the circuit might enter an undefined state, leading to unpredictable behavior (e.g., it could register as either logic 1 or logic 0).

<img width="866" height="486" alt="Screenshot 2025-07-17 194137" src="https://github.com/user-attachments/assets/87a506ed-dbee-45a9-8d62-820ab90d4e43" />

Similarly, when all capacitors that were at 0 volts need to charge to Vdd through a single Vdd tap point, it causes a momentary lowering of the voltage at that Vdd tap point. As long as this voltage drop remains within the noise margin, the system functions correctly. However, if it ventures into an undefined region, the system's behavior becomes unpredictable.

<img width="863" height="477" alt="Screenshot 2025-07-17 194151" src="https://github.com/user-attachments/assets/03e61977-9345-4e56-8a57-5643b916f61f" />

The observed phenomena, which cause a reduction in the supply voltage, occur because power is supplied from a single point.

<img width="782" height="493" alt="Screenshot 2025-07-17 194208" src="https://github.com/user-attachments/assets/b4308245-5912-45b4-a7a3-2f6dd606e4bc" />

The solution to this problem is to use multiple power supplies. This involves creating a power mesh, where each block draws charge from its nearest power supply connection and similarly dumps charge to its nearest ground connection.

<img width="892" height="500" alt="Screenshot 2025-07-17 194226" src="https://github.com/user-attachments/assets/9d3a6397-5453-4d19-97cf-3990562f4436" />

The power planning strategy shown above depicts such a mesh.

#### Pin placement and logical cell placement blockage

**Pin Placement**
Consider the designs illustrated below that require implementation. The first circuit is driven by clk1, and the second by clk2, with respective inputs Din1 and Din2, and outputs Dout1 and Dout2. Additionally, we have pre-placed cells, such as BlockA, which receives inputs from Din1 and Din2, and BlockB, which receives inputs from clk1 and clk2 and provides a ClkOut.

Currently, this setup has 4 input ports (Din1, Din2, Clk1, Clk2) and 3 output ports (Dout1, ClkOut, Dout2).

<img width="741" height="398" alt="Screenshot 2025-07-17 194256" src="https://github.com/user-attachments/assets/0f2ddb06-272b-4924-8778-19eec196fda5" />

Let's consider another design requiring implementation. These types of circuits are particularly useful for understanding inter-clock timing analysis. The complete design, as shown below, now features 6 input ports and 5 output ports. The connectivity between gates is defined using HDL (VHDL/Verilog) and is referred to as the 'Netlist'.
 
<img width="560" height="491" alt="Screenshot 2025-07-17 194319" src="https://github.com/user-attachments/assets/c817cc82-08cb-4ff1-acc1-f960864addf4" />

We now take this netlist and place it within the core designed earlier. The empty space between the core and the die needs to be filled with pin information. The front-end team defines the netlist connectivity, inputs, and outputs, while the back-end team handles pin placements. According to pin placement guidelines, pre-placed blocks should be located closer to their respective input pins.

<img width="671" height="496" alt="Screenshot 2025-07-17 194341" src="https://github.com/user-attachments/assets/264ff2ef-4ee0-4b5d-9b25-9b980bed10f8" />

One notable observation is that clock input (clock-in) and clock output (clock-out) pins are larger than other input and output pins. This is because input clocks must continuously provide signals to every element on the chip, and output clocks need to transmit signals as quickly as possible. Therefore, clock paths require the least resistance. A larger pin size results in lower resistance.

Another crucial consideration is that the pin placement area is typically blocked for both routing and cell placements. This necessitates a logical cell placement blockage, as depicted in the image above between the pins.

<img width="725" height="486" alt="Screenshot 2025-07-17 194400" src="https://github.com/user-attachments/assets/939b747f-5a0f-4f0f-bce4-66d2292452ca" />

With these steps, the floorplan is now ready for the Placement and Routing stages.

#### Steps to run floorplan using OpenLANE

Before running floorplanning, specific switches (parameters) for the process need to be set. These can be found in the OpenLane configuration files.

<img width="952" height="1017" alt="Screenshot 2025-07-17 194802" src="https://github.com/user-attachments/assets/653aaadf-7ad7-438c-b22c-39f81a1895c6" />

As seen in the configuration, the core utilization ratio is 50% (by default), and the aspect ratio is 1 (by default). Other related information is also provided. However, these default values are not mandatory and can be modified based on specific design requirements.

The FP_PDN files define the power distribution network. These switches are automatically configured in the floorplan stage by default within OpenLANE.

<img width="961" height="1014" alt="Screenshot 2025-07-17 194906" src="https://github.com/user-attachments/assets/6b58400d-7121-4ab4-8fbf-05f7bdad662f" />

FP_IO_MODE 1 0 indicates that pin positioning is random but ensures equal spacing between pins.

In OpenLANE, the system defaults (e.g., floorplanning.tcl) have the lowest priority. The config.tcl file (at the design level) has the next priority, and the highest priority is given to the PDK variant's config.tcl (e.g., sky130A_sky130_fd_sc_hd_config.tcl).

Now, let's examine how the floorplan runs with these settings.

#### Review floorplan files and steps to view floorplan

Inside the run folder, you'll find a config.tcl file. This file contains all the configurations adopted by the current flow. Opening it allows you to verify which parameters were active during the current run.

<img width="957" height="1019" alt="Screenshot 2025-07-17 195019" src="https://github.com/user-attachments/assets/b9450f6a-67b9-4966-9520-ba6f85df36e3" />

<img width="961" height="1014" alt="Screenshot 2025-07-17 194906" src="https://github.com/user-attachments/assets/a9e283da-1b62-4cef-bef1-b01d605864cc" />


To visualize the floorplan layout, navigate to the results folder. Here, a .def (Design Exchange Format) file is available. Opening this file reveals detailed information such as the die area (e.g., (0 0) to (660685 671405)) and the unit distance in microns (e.g., 1000, meaning 1 micron equals 1000 database units). By dividing the die dimensions (660685 and 671405) by 1000, you can obtain the chip's dimensions in micrometers.

<img width="955" height="1018" alt="Screenshot 2025-07-17 195623" src="https://github.com/user-attachments/assets/7a34f6d3-27b3-4187-986a-0f99de30339d" />

So, for instance, the chip's width would be 660.685 micrometers, and its height would be 671.405 micrometers.

To view the actual layout after the flow, open the Magic file using the command:

```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def
```
After pressing Enter, the Magic file will open, displaying the layout.

<img width="953" height="1027" alt="Screenshot 2025-07-17 195852" src="https://github.com/user-attachments/assets/1549f4dc-6058-4db5-b600-f63dfe615ab5" />

#### Review floorplan layout in Magic

In the Magic layout, you can observe that the input and output pins are positioned at equal distances.

<img width="957" height="1016" alt="Screenshot 2025-07-17 195952" src="https://github.com/user-attachments/assets/dc35a0d5-7904-4b63-9914-82dcc81418be" />

To inspect a specific input pin (select by clicking on it and pressing 's' on the keyboard; zoom in with 'z', zoom out with 'shift+z'), open the tkcon window and type `what`. This command will display detailed information about that particular pin.

<img width="955" height="1011" alt="Screenshot 2025-07-17 200113" src="https://github.com/user-attachments/assets/2cce31fe-b82b-44c0-9ed7-55e95f6453ab" />

Additionally, Decap cells (Decoupling Capacitors) are arranged along the borders of the side rows.

<img width="961" height="1014" alt="Screenshot 2025-07-17 200327" src="https://github.com/user-attachments/assets/e6ac120e-cd2d-4edf-bbfa-fc7df3e1b0ab" />

Here, you can distinguish different standard cells, such as Buffer 1, Buffer 2, AND gates, and so on.

<img width="714" height="362" alt="Screenshot 2025-07-17 200536" src="https://github.com/user-attachments/assets/f0d17ab7-4f3d-4d80-a4e6-03d4bcb48e42" />

#### Library building and Placement

**Netlist binding and initial place design**
Bind netlist with physical cells:
A netlist logically describes gates (e.g., a NOT gate as a triangle). In reality, these gates are physical boxes with defined width and height, like square boxes for AND gates or flip-flops.
Each component of the netlist is assigned a specific physical shape and dimensions because abstract shapes (like graphical AND/OR gates) do not exist in the real world. All blocks also possess defined width, height, and proper physical form.

<img width="884" height="496" alt="Screenshot 2025-07-17 200718" src="https://github.com/user-attachments/assets/467664d5-6d85-4fb7-bd83-189257710fe8" />

After removing the wires, all the gates, flip-flops, and blocks are conceptually available in a collection called the Library.
A Library functions like a physical library: it houses various "books" (gates, flip-flops) and provides their timing information (e.g., gate delays). A library can be structured into sub-libraries, perhaps one containing shape and size information, and another solely containing delay data.
Crucially, a library typically offers multiple "flavors" for each cell; the same cell might have a larger physical size in a different library section. Larger cells generally offer lower resistance paths, leading to faster operation and reduced delay. Designers can select cells based on timing conditions and available space on the floorplan.

<img width="890" height="498" alt="Screenshot 2025-07-17 200729" src="https://github.com/user-attachments/assets/a682ac9c-709b-4334-8531-dcafc49af5aa" />

**Placement:**
Once each gate has been assigned its proper physical shape and size, the next step is to place these physical representations onto the floorplan.
We begin with the floorplan, which includes defined input/output ports and a specific netlist where each component has a defined size. This gives us a physical view of the logic gates.
The placement process involves taking the connectivity information from the netlist and arranging the physical gate views onto the floorplan.

<img width="897" height="503" alt="Screenshot 2025-07-17 200742" src="https://github.com/user-attachments/assets/669a363b-a784-4b71-80f8-702c2d64196c" />

Placement tools ensure that previously pre-placed cells (from earlier stages) retain their fixed locations and that no new cells are placed on top of them. The primary objective is to arrange the netlist's physical components on the floorplan such that logical connectivity is preserved, interactions with I/O ports are optimized for timing, and overall delay is minimized.

<img width="884" height="506" alt="Screenshot 2025-07-17 200756" src="https://github.com/user-attachments/assets/e53a3f61-421d-4837-8b5e-c1f160437142" />

Initially, the remaining netlist components are arranged on the floorplan. While most elements are placed close to their I/O pins, some, like FF1 of Stage 4 relative to Din4, may still be distant. This distance problem can be resolved through placement optimization.

<img width="887" height="484" alt="Screenshot 2025-07-17 201051" src="https://github.com/user-attachments/assets/d52a0782-e30b-4dc9-8ca1-3da0bc55a5a6" />

#### Optimize placement using estimated wire-length and capacitance

**Optimize Placement:** This phase aims to resolve spacing issues and optimize interconnections.
Consider the connection from FF1 to Din2. If a wire directly connects them, its length could be considerable, leading to high capacitance and resistance. Sending a signal over such a long wire would make it difficult for FF1 to receive the input reliably due to signal degradation.
To maintain signal integrity over long distances, intermediate steps are introduced. These are called Repeaters, which are essentially buffers. Repeaters recondition the original signal, create a new, clean replica, and forward it. This process repeats until the signal successfully reaches the target cell.
While repeaters solve signal integrity issues, they consume additional area on the floorplan, as more repeaters mean more occupied space.

<img width="889" height="493" alt="Screenshot 2025-07-17 201119" src="https://github.com/user-attachments/assets/ef5deb3b-5f1d-4056-8e8c-29762d5fcef4" />

In Stage 1, a signal might not require any repeaters. However, in Stage 2, due to a significant distance, the wire length is high, and the signal cannot be transmitted reliably within the desired range, thus requiring a repeater.

<img width="900" height="497" alt="Screenshot 2025-07-17 201147" src="https://github.com/user-attachments/assets/9c1ff5f3-a7a6-479a-acf1-3339eb5233e7" />

#### Final placement optimization

Similar to Stage 2, Stage 3 also requires a buffer between Gate2 and FF2.

<img width="889" height="490" alt="Screenshot 2025-07-17 201210" src="https://github.com/user-attachments/assets/c918b53d-92c9-43a1-9c7e-22376af1f032" />

Stage 4 presents more complexity compared to other stages. To verify the correctness of our actions, we need to perform Timing Analysis using ideal clocks. Based on the analysis data, we can determine if the placement is correct.

<img width="896" height="496" alt="Screenshot 2025-07-17 201229" src="https://github.com/user-attachments/assets/59906110-1120-408a-9c8f-e1e9c6c94991" />

#### Need for libraries and characterization

Every IC design flow involves several steps. The first is Logic Synthesis: converting a functional description (RTL) into a legal hardware representation, resulting in an arrangement of gates that implements the original RTL functionality.
The next step, Floorplanning, imports the synthesis output and defines the core and die sizes.
Following floorplanning is Placement, where logic cells are arranged on the chip to achieve optimal initial timing.
CTS (Clock Tree Synthesis) ensures that the clock signal reaches every sequential element simultaneously and that each clock signal maintains equal rise and fall times.
Routing is the subsequent step, dependent on the characterization of flip-flops.
Finally, STA (Static Timing Analysis) examines setup time, hold time, and the maximum achievable frequency of the circuit.
A common element across all these stages is the use of 'GATES or Cells'.

#### Congestion aware placement using RePlAce

At this stage, our primary constraint is congestion, not timing. Our objective is to minimize congestion.
Placement is executed in two stages: Global and Detailed. Legalization (ensuring cells conform to grid and rule constraints) does not occur during global placement but is performed after detailed placement.
When placement is initiated, global placement runs first, primarily aiming to reduce wire length.

Now, let's open the Magic file to view the actual standard cell placement.

<img width="954" height="1016" alt="Screenshot 2025-07-17 201526" src="https://github.com/user-attachments/assets/65facdfc-dfe9-4f96-b48a-21046cbef3d5" />

The actual view in the Magic file is shown above.
Zooming into this view, you can identify various components like buffers, gates, and flip-flops.

<img width="955" height="1017" alt="Screenshot 2025-07-17 201608" src="https://github.com/user-attachments/assets/d3ef2d53-0cc8-4423-aba5-9f29f2e40116" />

#### Cell design and characterization flows

**Inputs for cell design flow**
In the Cell Design Flow, gates, flip-flops, and buffers are referred to as 'Standard Cells'. These standard cells are stored in a section called the 'Library'.
Within the library, numerous other cells are available, sharing the same functionality but varying in size.

<img width="884" height="479" alt="Screenshot 2025-07-17 201840" src="https://github.com/user-attachments/assets/a5a4e90f-bcd2-49f5-a5b5-0ef23fabb5d5" />

The cell design flow for an inverter (from the library) typically involves the following steps:
An inverter must be represented in terms of its physical shape, drive strength, power characteristics, and so on.
Cell design flow is generally divided into three parts:

* Inputs
* Design steps
* Outputs

**1) Inputs:**
Inputs required for cell design include: PDKs (Process Design Kits), DRC (Design Rule Check) and LVS (Layout Versus Schematic) rules, SPICE models, a library, and user-defined specifications.
The DRC & LVS rules are provided in a technology file, which contains design rules and actual values. These rules can be converted into code.
A SPICE model provides information like the threshold voltage equation for transistors.

<img width="888" height="485" alt="Screenshot 2025-07-17 201857" src="https://github.com/user-attachments/assets/cf794f0b-1bbd-4c3f-b0ef-a560e463701a" />

**Circuit design steps**
The separation between the power rail and the ground rail defines the cell height. Cell width, on the other hand, depends on timing requirements and drive strength.

**2) Design steps:** Design typically involves three primary steps:

* Circuit design
* Layout design
* Characterization

In Circuit Design, there are two main steps:

* Implementing the core function itself.
* Modeling the PMOS and NMOS transistors to meet library specifications.

**3) Outputs:**
The typical outputs from the circuit design phase include:

* CDL (Circuit Description Language) file
* GDSII (Graphic Design System II) file
* LEF (Library Exchange Format) file
* Extracted SPICE netlist (.cir) file

<img width="874" height="496" alt="Screenshot 2025-07-17 201952" src="https://github.com/user-attachments/assets/a2ad4541-7ac8-4851-a4cc-08e24c717df0" />

**Layout design step**
In Layout Design, the first step is to implement the circuit's function using MOS transistors (a set of PMOS and NMOS transistors).
The second step involves extracting the PMOS network graph and the NMOS network graph from the implemented design.

<img width="915" height="497" alt="Screenshot 2025-07-17 202026" src="https://github.com/user-attachments/assets/f84ed3fc-cd14-48e5-8e7d-879c6a3b2b1e" />

After obtaining the network graphs, the next step is to derive Euler's path. Euler's path is essentially a path that traverses each edge of a graph exactly once.

<img width="891" height="487" alt="Screenshot 2025-07-17 202053" src="https://github.com/user-attachments/assets/f0250647-9925-4055-b683-e6046a875548" />

The subsequent step is to draw a stick diagram based on Euler's path. This stick diagram is derived from the circuit diagram.

<img width="492" height="301" alt="Screenshot 2025-07-17 202133" src="https://github.com/user-attachments/assets/e8c6e20a-42d0-4329-a91b-aeab9bd762a4" />

The next crucial step is to convert this stick diagram into a proper Layout, applying the appropriate design rules discussed earlier. Once the specific layout is achieved, details such as cell width, cell length, and all other specifications (like drain current, pin locations, etc.) will be defined.

<img width="282" height="321" alt="Screenshot 2025-07-17 202211" src="https://github.com/user-attachments/assets/9691a70b-fbf0-4928-8734-b8a21e40d392" />

The next and final step is to extract the parasitics of that particular layout and characterize it in terms of timing. The output of the layout design phase is the GDSII file. Once the extracted SPICE netlist is obtained, it is characterized. Characterization helps in obtaining detailed timing, noise, and power information.

#### Typical characterization flow

Let's outline a typical characterization flow based on the inputs we have:

1. Read in the model.
2. Read the extracted SPICE netlist.
3. Define or recognize the behavior of the buffer.
4. Read the subcircuits of the inverter.
5. Attach necessary power supplies.
6. Apply stimulus.
7. Provide the necessary output capacitance.
8. Provide the necessary simulation command (e.g., .tran for transient simulation, .dc for DC simulation).

<img width="762" height="420" alt="Screenshot 2025-07-17 202238" src="https://github.com/user-attachments/assets/b5f7b4b6-ed15-470d-943a-bb20554e2bbc" />

The next step involves feeding all these inputs (steps 1 to 8) in the form of a configuration file to the characterization software, typically named "GUNA".

This software then generates the power, noise, and timing models.

<img width="883" height="501" alt="Screenshot 2025-07-17 202319" src="https://github.com/user-attachments/assets/cc970ef5-e218-4649-a6dc-9ae230c51aab" />

#### General timing characterization parameters

**Timing threshold definitions**
As seen in the previous section, with inverters connected back-to-back, power sources, and applied stimulus, it becomes critical to understand different threshold points of a waveform. These are called "Timing threshold definitions."
In the figure below, the term Slew_low_rise_thr depicts a value close to 0, typically around 20%, but it could also be 30%.

<img width="880" height="486" alt="Screenshot 2025-07-17 202352" src="https://github.com/user-attachments/assets/647ff7b9-6d7d-47b1-b71e-17cc5914f71e" />

* Slew_high_rise_thr

<img width="886" height="503" alt="Screenshot 2025-07-17 202410" src="https://github.com/user-attachments/assets/30bff620-83eb-4641-a83b-ec9a73fbb57b" />

* Slew_low_fall_thr

<img width="887" height="502" alt="Screenshot 2025-07-17 202453" src="https://github.com/user-attachments/assets/1e06e570-2e48-4c1e-a711-521042a6c4e9" />

* Slew_high_fall_thr

<img width="887" height="501" alt="Screenshot 2025-07-17 202509" src="https://github.com/user-attachments/assets/bf777198-7d61-4ce5-9879-2b3d9a2fcea6" />

Now, considering the waveform of the input stimulus (input to the first buffer) and the output of the first buffer, thresholds for delay are also available, similar to slew thresholds. For delay, these thresholds are typically around 50%.

* in_rise_thr

<img width="873" height="486" alt="Screenshot 2025-07-17 202535" src="https://github.com/user-attachments/assets/d651bc0e-f50f-426e-a91b-0e19588edaf6" />

* in_fall_thr

Its typical value is 50%.

<img width="887" height="504" alt="Screenshot 2025-07-17 202613" src="https://github.com/user-attachments/assets/875b7b44-31c8-4f2e-947f-8ebce69686cd" />

* out_rise_thr

<img width="890" height="496" alt="Screenshot 2025-07-17 202624" src="https://github.com/user-attachments/assets/2f5dfb33-8535-409a-ac6d-2e84ecfca6cc" />

* out_fall_thr

<img width="882" height="497" alt="Screenshot 2025-07-17 202636" src="https://github.com/user-attachments/assets/f1ee572e-afa5-4908-bf48-7c17f91f5d77" />

#### Propagation delay and transition time

Based on the above values, we calculate further parameters like propagation delay, current, and slews.
To calculate the delay of any signal, we subtract `out_rise_thr` from `in_rise_thr`. Taking a typical value of 50%, let's see how it works on a waveform:
Time delay = Time(out_thr) - Time(in_thr)

<img width="848" height="437" alt="Screenshot 2025-07-17 202733" src="https://github.com/user-attachments/assets/4f8a584a-c53a-4697-98da-eb129b8bd562" />

In the example above, `in_rise_thr` and `out_fall_thr` were set at 50%. However, if the threshold point shifts upwards, the output might appear before the input, resulting in a negative delay. Negative delays are generally unacceptable. The presence of negative delay indicates a poor choice of threshold point, highlighting its crucial importance.

Let's consider another example where the threshold point is chosen correctly, yet a negative delay can still occur. This happens because the output appears before the input, which is an unacceptable negative delay.

<img width="803" height="413" alt="Screenshot 2025-07-17 202749" src="https://github.com/user-attachments/assets/06ad1775-4cc2-4c4e-9655-98e9a948fe2b" />

Transition time is calculated as:
Transition time = Time(slew_high_rise_thr) - Time(slew_low_rise_thr)
OR
Transition time = Time(slew_high_fall_thr) - Time(slew_low_fall_thr)

Let's use a waveform to understand slew calculation.

<img width="838" height="403" alt="Screenshot 2025-07-17 202811" src="https://github.com/user-attachments/assets/f9133671-aec7-4e21-8478-da9f3457609e" />

---

### Day 3 - Design library cell using Magic Layout and ngspice characterization

#### Labs for CMOS inverter ngspice simulations

#### IO placer revision

Following floor planning and placement, we might need to modify the floorplan. For instance, if pins are currently placed at equal distances, we can adjust their positioning using the Set command.
To do this, first, review the configuration switches. Locate the FP_IO_MODE syntax, for example, `env(FP_IO_MODE) 1`, and change its value to 2. Then, re-run the floorplanning process.
Verify the changes in pin locations using `magic -T`.

[Image: Magic layout showing pins in the lower half]

As observed in the image, all pins are now concentrated in the lower half of the core, with no pins in the upper half.

#### SPICE deck creation for CMOS inverter

**VTC- SPICE simulations:** The initial step involves creating a SPICE deck. This deck fundamentally defines the netlist's connectivity, specifying the simulation inputs and output measurement points.

* **Component connectivity:** We define the connectivity of the substrate pin, which is crucial for tuning the threshold voltage of both PMOS and NMOS transistors.
* **Component values:** We assign specific values for the PMOS and NMOS transistors, typically taking them to be of the same size.
* **Identify the nodes:** Nodes represent the connection points between components. These nodes are essential for defining the netlist.
* **Name the nodes:** We then assign meaningful names to these nodes, such as Vin, Vss, Vdd, and out.

Now, we proceed to write the SPICE deck, following this format: Drain - Gate - Source - Substrate.

* For M1 MOSFET (PMOS): The drain connects to the out node, the gate to the in node, and both the substrate and source connect to the Vdd node.
* For M2 MOSFET (NMOS): The drain connects to the out node, the gate to the in node, and both the source and substrate connect to 0 (ground).

#### SPICE simulation lab for CMOS inverter

Having defined the CMOS inverter's connectivity, we now specify the connections for other components like the load capacitor and voltage sources.

* The output load capacitor is connected between the out node and node 0 (ground), with a value of 10fF.
* The supply voltage (Vdd) is connected between Vdd and node 0, with a value of 2.5V.
* Similarly, the input voltage (Vin) is connected between Vin and node 0, also with a value of 2.5V.

Next, we provide the simulation commands. We sweep the Vin from 0V to 2.5V in steps of 0.05V to observe Vout as Vin changes.

The final step involves incorporating the model files, which provide a complete description of the NMOS and PMOS transistors.
We then execute the SPICE simulation with these defined values to generate the voltage transfer characteristic (VTC) graph.

[Image: SPICE simulation VTC graph 1]

For a second simulation, we modify the PMOS width to be three times that of the NMOS width. After running this simulation, a new VTC graph is obtained.

[Image: SPICE simulation VTC graph 2 with modified PMOS width]

The key difference between these two graphs is that the second graph's transfer characteristic is precisely centered, whereas the first graph's characteristic is shifted to the left of the center.

#### Switching Threshold Vm

Both models, despite their different widths, have distinct applications. By comparing their waveforms, we observe that their shapes are identical, regardless of the voltage level. This demonstrates the inherent robustness of CMOS devices.

When the input voltage (Vin) is low, the output is high, and when Vin is high, the output is low. This fundamental characteristic is maintained across all CMOS inverters, irrespective of NMOS or PMOS sizing. This robustness is why CMOS logic is widely used in gate design.

The Switching Threshold, Vm, is a critical parameter that defines an inverter's robustness. It is the point where Vin equals Vout.

[Image: VTC graph showing Vm]

In this figure, Vm is approximately 0.9V, where Vin = Vout. This point is critical for CMOS operation because both PMOS and NMOS transistors have a chance of being simultaneously turned on. If both are on, there's a high probability of leakage current (current flowing directly from power to ground).

Comparing both graphs helps in understanding the concept of switching threshold voltage.

[Image: VTC graph showing PMOS/NMOS regions]

In the graph above, we can identify the operating regions for PMOS and NMOS. The current flows in different directions for NMOS and PMOS.

#### Static and dynamic simulation of CMOS inverter

Dynamic simulation provides insights into the rise and fall delays of a CMOS inverter and how they vary with Vm. In this simulation, all parameters remain constant except for the input, which is a pulse, and the simulation command, which is `.tran`.

The simulation will plot a Time vs. Voltage graph, from which we can calculate the rise and fall delays.

[Image: Dynamic simulation Time vs. Voltage graph]

#### Lab steps to git clone vsdstdcelldesign

To clone the repository, copy the clone address from the repository's page and paste it into the OpenLane terminal after the `git clone` command. This will create a folder named "vsdstdcelldesign" within your OpenLane directory.
If you check your OpenLane directory, you will now find the `vsdstdcelldesign` folder.
Navigating into the `vsdstdcelldesign` folder reveals files such as `.mag` files and `libs` files.
Before opening the `.mag` file to inspect the layers used for building the inverter, you need the technology file. Copy this file from the specified address using the `cp` command to the destination provided.

[Image: Terminal output showing file copy]

The output confirms that the file has been successfully copied into the `vsdstdcelldesign` folder.
Now, you can open the layout in Magic without needing to type the full tech file path, as it's locally copied.

[Image: Magic layout of CMOS inverter]

You can now view the CMOS inverter layout in Magic, as shown above.

#### Inception of layout & CMOS fabrication process

**Create Active regions**
1) **Selecting a substrate:** We start with a P-type silicon substrate, characterized by high resistivity (5-50 ohm) and a (100) orientation.

2) **Creating active region for transistor:** These are the regions where PMOS and NMOS transistors will be formed. On the P-type substrate, small pockets, known as active regions, are created to house these transistors. Isolation is established between each of these pockets.
The isolation layer is created by depositing a silicon dioxide (SiO2) layer (approximately 40nm thick) onto the substrate, followed by a silicon nitride (Si3N4) layer (around 80nm thick) on top of the SiO2.

Before creating the pockets, identify the precise regions where they are needed. Then, a photoresist layer (approximately 1um thick) is deposited, onto which Mask 1 is patterned using UV light.

[Image: Photoresist patterning with Mask 1]

Unwanted areas are exposed using UV light, and the exposed photoresist is subsequently washed away, leaving the desired pattern.

[Image: Photoresist pattern after washing]

In the next step, the remaining photoresist is removed, and the Si3N4 layer in the exposed areas is etched.

[Image: Etching Si3N4 layer]

Now, the photoresist is chemically removed, as the Si3N4 layer itself acts as a protective layer for the SiO2 underneath. The wafer is then placed in an oxidation furnace. If we perform the LOCOS (Local Oxidation of Silicon) process, the exposed SiO2 will grow, forming what is known as a "bird's beak." This grown SiO2 provides effective isolation between two PMOS and NMOS transistors, preventing unwanted communication between them.

[Image: LOCOS process showing SiO2 growth and bird's beak]

The final step in this phase is to remove the Si3N4 using hot phosphoric acid.

[Image: Si3N4 removal]

**Formation of N-well and P-well**
3) **N-well and P-well formation:** N-wells and P-wells cannot be formed simultaneously. One region must be protected by photoresist while the other is formed. Mask 2 and UV light are used to pattern the photoresist for P-well formation.

[Image: Mask 2 patterning for P-well]

The area intended for P-well formation is now exposed. The mask is removed, and Boron ions are implanted (at approximately 200keV) to create the P-implant. This is still a P-implant at this stage. High-temperature annealing is then performed to fully form the P-well.

[Image: P-implant formation and P-well]

A similar process is followed to form the N-well, using Mask 3 and Phosphorus ions.

[Image: Mask 3 patterning and N-well formation]

The depth of the wells is not yet defined. By subjecting the wafer to a high-temperature furnace (during drive-in diffusion), the desired depth of the wells is established.

**Formation of gate terminal**
4) **Gate formation:** The gate terminal is the most critical part of PMOS and NMOS transistors, as it controls the threshold voltage. Both the doping concentration and oxide capacitance influence the threshold voltage.
First, the doping concentration is controlled using Mask 4 and Boron ion implantation at lower energy (approximately 60keV).

[Image: Boron ion implantation for gate doping]

The same process is repeated for the N-well using Mask 5 and Arsenic ions.

[Image: Arsenic ion implantation for N-well gate doping]

Next, the oxide layer needs to be prepared. However, the existing oxide layer may have been damaged by previous processes. Therefore, the damaged layer is first removed using an HF solution, and then a new, high-quality oxide layer of the same thickness is re-grown.
The final step involves depositing a polysilicon layer over the oxide layer. This polysilicon is intentionally doped with more impurities to achieve a low-resistance gate terminal. This polysilicon layer is then etched using Mask 6 and photoresist.

[Image: Polysilicon etching with Mask 6]

After etching and removing the photoresist, the gate terminal takes its final shape.

[Image: Final gate terminal structure]

**Lightly doped drain (LDD) formation**
5) **LDD formation:** The objective here is to create specific doping profiles: P+, P-, N for PMOS and N+, N-, P for NMOS. This specific doping profile is crucial for mitigating two key effects:

* Hot electron effect
* Short channel effect

For LDD formation, ion implantation is performed in the P-well using Mask 7 and phosphorus as the lightly doping ion.

[Image: LDD implantation in P-well with Mask 7]

The same process is repeated for the N-well, using Mask 8 and Boron ions.

[Image: LDD implantation in N-well with Mask 8]

To protect the structure of the P-implant and N-implant, spacers are created. This involves depositing a thick SiO2 or Si3N4 layer over the gate terminal.

[Image: SiO2/Si3N4 deposition for spacers]

Subsequently, Plasma Anisotropic Etching is performed, leading to the formation of side-wall spacers.

[Image: Side-wall spacers formed after etching]

**Source & drain formation**
6) **Source-drain formation:**
The next step is to deposit a very thin screen oxide layer to prevent channeling effects.

[Image: Screen oxide layer deposition]

To form the drain and source, arsenic ions are again implanted at 75keV using Mask 9 in the P-well to create the N+ implant for PMOS.

[Image: N+ implant for PMOS Source/Drain]

The same process is repeated for NMOS, using Mask 10 and boron ions in the N-well at 50keV to create the P+ implant.

[Image: P+ implant for NMOS Source/Drain]

This partially fabricated CMOS is then subjected to high-temperature annealing (1000 degrees Celsius). During this step, the P+ implant and N+ implant regions fully form the source and drain terminals.

[Image: Annealing process showing Source/Drain formation]

**Local interconnect formation**
7) **Steps to form contacts and local interconnects:**
The first step is to remove the thin screen oxide layer through etching. Then, titanium (Ti) is deposited using sputtering. Titanium is chosen for its very low resistivity.

[Image: Titanium deposition]

The next step involves a reaction between the Ti layer and the source, gate, and drain regions of the CMOS. This is achieved by heating the wafer to approximately 650-700 degrees Celsius in an N2 ambient for about 60 seconds. After the reaction, titanium silicide is formed over the wafer. Another reaction occurs between Ti and N, resulting in TiN (Titanium Nitride), which is used for local communication.

[Image: Titanium silicide and TiN formation]

Using Mask 11 and photoresist, the TiN layer is etched to create specific contacts. The etching of TiN is completed using RCA cleaning.

[Image: TiN etching and contact formation]

After etching and removing the photoresist, the local interconnects are fully formed.

[Image: Final local interconnects]

**Higher level metal formation**
8) **Higher level metal formation:** These steps are very similar to the previous ones. The first thing to note is that the surface is currently non-planar. This non-planar surface is unsuitable for metal interconnects due to potential problems with metal discontinuity. Therefore, the surface must be planarized. This is done by depositing a thick layer of SiO2 with some impurities to make it less resistive, followed by CMP (Chemical Mechanical Polishing) to achieve a planar surface.

[Image: Planarization using SiO2 and CMP]

Now, using Mask 12 and photoresist, the SiO2 layer is etched to prepare for metal deposition.

[Image: SiO2 etching for metal deposition]

After removing the photoresist, a thin layer of TiN (approximately 10nm) is deposited over the wafer. TiN acts as an excellent adhesion layer for SiO2 and also serves as a barrier between the bottom and top layers of metal interconnects.

[Image: TiN deposition]

The next step involves depositing a blanket tungsten (W) layer over the wafer, followed by CMP to planarize the surface.

[Image: Tungsten deposition and CMP]

This tungsten layer forms contact holes, which need to connect to the higher metal layers. Therefore, an Aluminum (Al) layer is then deposited.

[Image: Aluminum layer deposition]

Using Mask 13 and photoresist, the tungsten layer is etched to form contacts at specific locations via Plasma etching.

[Image: Tungsten etching for contacts]

This completes our first level of metal interconnects. The same process is repeated to deposit the second level of metal interconnects, using Mask 14 for etching SiO2 and Mask 15 for etching the Al layer.

[Image: Second level metal interconnect formation]

The upper Al layer is typically thicker compared to the lower Al layer. Finally, another layer of SiO2 or Si3N4 is deposited to protect the chip.

[Image: Final protective layer]

And finally, our CMOS looks like this after the fabrication process.

[Image: Final fabricated CMOS device]

#### Lab introduction to Sky130 basic layers layout and LEF using inverter

In Sky130, each color represents a different layer. The first layer, local interconnect, is shown in blue-purple. Metal 1 is light purple, and Metal 2 is pink. N-well is depicted by a solid dashed line, green for the N-diffusion region, and red for the polysilicon gate. Similarly, brown indicates the P-diffusion.
In the tkcon window, you can select an area (e.g., NMOS) and verify its details. You can perform similar checks for PMOS to ensure the CMOS is functioning correctly.

[Image: tkcon output showing NMOS details]

You can also check the output terminal by double-pressing "S" to select the entire output "Y".

[Image: tkcon output for output terminal "Y"]

The output confirms that "Y" is attached to locali in the cell definition sky130_inv.
You can verify if the source of the PMOS is connected to ground, and similarly for the NMOS.

#### Lab steps to create std cell layout and extract spice netlist

To extract the file, type the command `extract all` in the tkcon window.

[Image: tkcon command for extraction]

Navigate to this location from the terminal to find the extracted file.

[Image: Terminal output showing extracted file]

We will use this `.ext` file to create a SPICE file compatible with the ngspice tool. For this, first apply the command `ext2spice cthresh 0 rthresh 0`. This command itself will not create a new file. Then, type the `ext2spice` command again in the tkcon window.

[Image: tkcon commands for ext2spice]

Now, check the specified location to find the newly created SPICE file.

[Image: Terminal output showing SPICE file creation]

To view the contents of the SPICE file, use `vim sky130_inv.spice`.

[Image: Contents of sky130_inv.spice]

#### Sky130 Tech File Labs

#### Lab steps to create final SPICE deck using Sky130 tech

In the SPICE deck, you can see all the details regarding the connectivity of the NMOS and PMOS transistors, as well as the power supply.
X0 represents the NMOS, and X1 represents the PMOS. Their connectivity is shown as GATE-DRAIN-SUBSTRATE-SOURCE.

[Image: SPICE deck details]

Now, we need to include the PMOS and NMOS library files, which are located inside the `libs` folder within the `vsdstdcellsdesign` directory.

[Image: Library file paths]

Include these files in the terminal using the commands `.include ./libs/pshort.lib` and `.include ./libs/nshort.lib`.
Set the supply voltage VDD to 3.3V using the command `VDD VPWR 0 3.3V`. Similarly, set the value for VSS.
Next, specify the input signals, for example: `Va A VGND PULSE(0V 3.3V 0 0.1ns 2ns 4ns)`.
Also, include simulation analysis commands like `.tran 1n 20n`, `.control`, `run`, `.endc`, and `.end`.

After running this file, you will get the output from ngspice.

[Image: ngspice output]

Now, plot the graph using the command `plot y vs time a`.

[Image: Initial VTC plot]

If you increase the C3 value from 0.024fF to 2fF, the graph becomes smoother, as shown below.

[Image: Smoother VTC plot with increased C3]

#### Lab steps to characterize inverter using sky130 model files

Here, we aim to find the values for four key parameters:

* Rise Time
* Fall Time
* Propagation Delay
* Cell Fall Delay

**Rise Time:** This is the time taken for the output waveform to transition from 20% to 80% of its final value.

[Image: Waveform illustrating rise time calculation]

So, the rise time = (2.2489 - 2.1819)e-09 = 66.92 psec.

**Fall Time:** This is the time taken for the output waveform to transition from 80% to 20% of its initial value.

[Image: Waveform illustrating fall time calculation]

So, the fall time = (4.09512 - 4.05264)e-09 = 42.51 psec.

**Propagation Delay:** This is the time difference between the 50% point of the input waveform and the 50% point of the output waveform.

[Image: Waveform illustrating propagation delay calculation]

So, the propagation delay = (2.2106 - 2.15012)e-09 = 60.48 psec.

**Cell Fall Delay:** This is the time taken for the output to fall to 50% when the input is rising to 50%.

[Image: Waveform illustrating cell fall delay calculation]

So, the cell fall delay = (4.07735 - 4.04988)e-09 = 27.47 psec.
We have successfully characterized our inverter. Our next objective is to create a LEF file using the layout, which we will then integrate into the picorv32a core.

#### Lab introduction to Magic tool options and DRC rules

For more information about Magic DRC, refer to: [http://opencircuitdesign.com/magic/Technologyfiles/TheMagicTechnologyFileManual/DrcSection](http://opencircuitdesign.com/magic/Technologyfiles/TheMagicTechnologyFileManual/DrcSection)
Link to Google SkyWater Design Rules: [https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)
For reference, you can use the GitHub repository of Google-SkyWater: [https://github.com/google/skywater-pdk](https://github.com/google/skywater-pdk)

#### Lab introduction to Sky130 pdk's and steps to download labs

Follow these steps:

1.  Go to the home directory.
2.  To download the lab files for performing DRC corrections, use:

    ```bash
    wget [http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz](http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz)
    ```

3.  To extract the lab files from the downloaded archive:

    ```bash
    tar xfz drc_tests.tgz
    ```

4.  Then, navigate into the `drc_tests` lab folder.
5.  To list all directories, use the command:

    ```bash
    ls -al
    ```

6.  To view the `.magicrc` file, use the command `gvim .magicrc`. This file serves as the startup script for Magic, instructing it where to find the technology file. Since the technology file is already available locally in the same directory, you can make changes to it if needed.
7.  To start the Magic tool with enhanced graphics, use the command:

    ```bash
    magic -d XR &
    ```

[Image: Content of .magicrc file]

The content of the `.magicrc` file using the `vi .magicrc` command is shown above.

#### Lab introduction to Magic and steps to load Sky130 tech-rules

Use the command `magic -d XR` to open the Magic tool.
Open the `met3.mag` file from the file menu. You will observe different layouts with varying DRC values, identified by rule numbers.

[Image: Magic layout with DRC rule numbers]

These rule numbers can be found in the Google-SkyWater documentation.

[Image: Google-SkyWater documentation showing rule numbers]

Now, select any layout area and check for DRC violations using `drc why` in the tkcon window.

[Image: tkcon output from drc why command]

Next, select a blank area and hover the mouse pointer over the metal3 contact icon. Press the 'p' button and type 'pek' in the tkcon. Then execute the command `cif see VIA2` in the tkcon tab.
You will observe a series of black squares appearing inside the area.

[Image: Magic layout after cif see VIA2 command]

#### Lab exercise to fix poly.9 error in Sky130 tech-file

Now, open the `poly.mag` file in the Magic tool using the command `load poly.mag` in the tkcon terminal.

[Image: Magic layout for poly.mag]

Consider the rule poly.9 and consult the website for details on this specific rule.

[Image: Website content for poly.9 rule]

To identify the error, examine the `sky130A.tech` file, located in the `drc_tests` directory. You can open this file with a Linux text editor.

[Image: sky130A.tech file content]

Search for 'poly.9' within the `sky130A.tech` file. It appears in both the POLY and uhrpoly sections, where the rules are incorrectly defined. Make the necessary changes in both sections.

[Image: Modified sky130A.tech content]

After modifying the `sky130A.tech` file, save and close the editor.
Next, execute the command `tech load sky130A.tech` in the tkcon terminal. Then, run the DRC check as shown below.

[Image: DRC check command and output]

#### Lab exercise to implement poly resistor spacing to diff and tap

To correctly implement poly resistor spacing, you will need to modify the `sky130A.tech` file again.

[Image: sky130A.tech content for poly resistor spacing]

Now, execute the necessary commands in Tkcon after saving the file.

[Image: tkcon output after executing commands]

To check for errors, you can create a copy of the poly.9 model from the `poly.mag` file within the Magic window.

[Image: Magic window showing poly.9 model copy]

To find the description of a DRC error, select the area containing the error in the Magic window, then run the command `drc why` in the tkcon terminal.
This command will provide a description of the error.

[Image: tkcon output with DRC error description]

#### Lab challenge exercise to describe DRC error as geometrical construct

Now, we will make the following changes in the `sky130A.tech` file:

[Image: sky130A.tech content for nwell.6 modification]

To locate the nwell.6 model error, open the `nwell.mag` file in the Magic tool. In the figure, the deep n-well is depicted by yellow stripes, and the n-well by a dotted green pattern.

[Image: nwell.mag showing deep n-well and n-well]

This error can also be observed directly at the site.

[Image: Error visible at site]

#### Lab challenge to find missing or incorrect rules and fix them

Now, open the Magic tool and execute the commands `drc style drc(full)` and `drc check`.

[Image: Magic commands for DRC check]

---

### Day 4 - Pre-layout timing analysis and importance of good clock tree

#### Timing modeling using delay tables

#### Lab steps to convert grid info to track info

We need to extract the .lef file from the .mag file to integrate it into the picorv32a flow.
When creating standard cells, specific guidelines must be followed:
* Input and output ports must align with the intersections of vertical and horizontal tracks.
* The standard cell's width should be an odd multiple of the track pitch, and its height an odd multiple of the track vertical pitch.

More detailed information can be found by opening the track file located at `pdk/sky130/libs.tech/openlane/sky130_fd_sc_hd/track.info`.

<img width="952" height="1017" alt="Screenshot 2025-07-20 014714" src="https://github.com/user-attachments/assets/9f8074d1-aba1-4934-bbd7-6051e960783f" />

Tracks are essential during the routing stage, serving as defined paths for metal layers (e.g., Metal 1, Metal 2).
Since Place & Route (PNR) is an automated process, we must specify the intended routing paths, which are provided by these tracks. Each track is positioned at specific coordinates: (0.23, 0.46)µm horizontally and (0.17, 0.34)µm vertically for li1, Metal 1, and Metal 2 layers.
In the layout, ports reside on the li1 layer. To ensure these ports intersect with the tracks, we need to convert the grid information into track information.

To achieve this, first open the tracks file, then open the tkcon window and type the `help grid` command.

<img width="959" height="1013" alt="Screenshot 2025-07-20 125929" src="https://github.com/user-attachments/assets/d2aa14f8-1d30-4aaf-802e-5602585ddc47" />

Subsequently, input the required commands based on the track file's specifications.

<img width="959" height="1017" alt="Screenshot 2025-07-20 130250" src="https://github.com/user-attachments/assets/c6735ae5-b19e-4474-9caa-02948c50c7c0" />

Upon completion, we can observe that the ports are correctly placed at the track intersections. Additionally, the second requirement (covering 3 boxes between boundaries) is also satisfied.

#### Lab steps to convert magic layout to std cell LEF

Next, we need to define the port names and their corresponding values. Values can be set for different ports. For power and ground ports, the 'attach to layer' property must be set to Metal1.

<img width="955" height="1018" alt="Screenshot 2025-07-20 133021" src="https://github.com/user-attachments/assets/d1fe21fa-a3d1-4a47-9fab-ad83d47d92f4" />

Once these parameters are configured, we are ready to extract the LEF file from the Magic layout.

<img width="956" height="1021" alt="Screenshot 2025-07-20 133458" src="https://github.com/user-attachments/assets/6598c251-4995-4574-8a4e-2847d01dda8d" />

To open the Magic file, use the command:

```bash
magic -T sky130A.tech sky130_vsdinv.mag &
```

To extract the LEF file, type the following command in the tkcon window:

```bash
lef write
```

This command will create a `.lef` file, which can be verified in the `vsdstdcellsdesign` folder using the `ls -ltr` command.

<img width="954" height="1015" alt="Screenshot 2025-07-20 133723" src="https://github.com/user-attachments/assets/29c25620-d475-41af-9dde-cc851b314842" />

#### Introduction to timing libs and steps to include new cell in synthesis

After creating the `.lef` file, the next step is to integrate it into the picorv32a flow. Before that, the file needs to be moved to the src folder, where all design files are consolidated.
The file can be copied using the `cp` command.

<img width="960" height="1014" alt="Screenshot 2025-07-20 162911" src="https://github.com/user-attachments/assets/16aa1a08-f88c-4cd0-a5e1-aa3fcc2faafa" />

The library file typically appears as shown above, with different versions like typical, slow, and fast.

<img width="958" height="1013" alt="Screenshot 2025-07-20 163342" src="https://github.com/user-attachments/assets/fc58a265-4354-447b-b3cf-a33b856032ce" />

Now, copy the file to the src folder.

<img width="958" height="1016" alt="Screenshot 2025-07-20 163754" src="https://github.com/user-attachments/assets/afd067f4-2017-41fa-8a61-9886a29126e8" />

We must then modify the `config.tcl` file within the `picorv32a` directory. Open this file and add the commands shown in the image below:

<img width="956" height="1013" alt="Screenshot 2025-07-20 170504" src="https://github.com/user-attachments/assets/6ef10e25-5f89-4225-b28a-8a0f8b7808ae" />

**OPENLANE:** Next, navigate to the OpenLane directory and execute the docker command.
Execute the following commands sequentially:

```bash
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]      
add_lefs -src $lefs
run_synthesis
```

<img width="959" height="1013" alt="Screenshot 2025-07-20 170638" src="https://github.com/user-attachments/assets/4222400e-e7d5-46f0-ac8c-a19d543436de" />

<img width="960" height="1012" alt="Screenshot 2025-07-20 170655" src="https://github.com/user-attachments/assets/29ec095d-0e8e-498f-8318-8e40d6064c50" />

<img width="958" height="1020" alt="Screenshot 2025-07-20 171205" src="https://github.com/user-attachments/assets/d58cc8c9-757a-4990-b170-e317bcc6e890" />

#### Introduction to delay tables

**Power Aware CTS:** In an AND gate, if the enable pin is logic '1', the clock signal propagates. If it's logic '0', the clock is blocked. Similarly, in an OR gate, if the enable is 'logic 0', the clock propagates, but if it's 'logic 1', the clock is blocked.
This blocking mechanism offers the significant advantage of saving substantial power within the clock tree.

<img width="543" height="324" alt="Screenshot 2025-07-20 193510" src="https://github.com/user-attachments/assets/e8fb33d0-9098-4055-bd93-e02981579a24" />

Consider a clock tree where a buffer at the first input drives the load of two subsequent buffers. If we split this buffer and replace it with an AND gate using a clock gating technique, we need to analyze if other circuit characteristics remain constant or change.

<img width="788" height="273" alt="Screenshot 2025-07-20 194038" src="https://github.com/user-attachments/assets/b8e4fcd0-24b4-4e6d-97f2-9eed6beccee5" />

Before swapping the buffer with a gate, we make the following assumptions:

<img width="308" height="252" alt="Screenshot 2025-07-20 194556" src="https://github.com/user-attachments/assets/8989f9e3-1bd2-43ad-9032-35369cfa896c" />

* Assume C1=C2=C3=C4=25fF
* Assume Cbuf1=Cbuf2=30fF
* Total Capacitance at node 'A' => 60fF
* Total Capacitance at node 'B' => 50fF
* Total Capacitance at node 'C' => 50fF

Based on these, we make the following observations:
* There are 2 levels of buffering.
* At every level, each node drives the same load.
* Identical buffers are used at the same level.

However, the output capacitance of the buffer for the entire circuit is not constant; the load at the output varies. Consequently, the input transition also varies.
This variation in output and input leads to a variety of delays. We will see how to capture these delays using delay tables.

#### How delay tables are prepared?

To prepare delay tables, a single buffer is taken from the circuit. Its input transition is varied within a specific range (e.g., 10ps-100ps). The output load will also vary accordingly. The delay is then characterized for these varying conditions, and the data is organized in a tabular format.

<img width="383" height="221" alt="Screenshot 2025-07-20 195336" src="https://github.com/user-attachments/assets/29dc56a9-0d1b-48c8-a8eb-b6222eca2c50" />

#### Delay table usage Part 1

Let's consider an example for other buffers.

<img width="844" height="216" alt="Screenshot 2025-07-20 200209" src="https://github.com/user-attachments/assets/ba62f108-d947-40ab-8867-bfab2b457276" />

For a practical scenario, assume Buffer 1 has an input transition of 40ps and an output capacitance of 60fF. In this case, the cell's delay falls between x9 and x10 in the delay table.
Values not explicitly present in the delay table are extrapolated from the given data, allowing for a range estimation.

#### Delay table usage Part 2

Now, we calculate the delay of Buffer 2 to determine the latency at four clock endpoints.
Assuming the input transition is common for both buffers, approximately 60psec, and the load at both buffers is 50fF, this results in a delay of y15.
The total delay from input to output is x9' + y15 (ignoring wire delays). This implies that the skew at any output point is zero.
If the load is not uniform across all nodes, the skew will not be zero.

#### Lab steps to configure synthesis settings to fix slack and include vsdinv

We will modify the parameters of our cell by referring to the `README.md` file located in the OpenLane directory's configuration folder. This file contains information about various cell parameters.

<img width="960" height="1018" alt="Screenshot 2025-07-20 210136" src="https://github.com/user-attachments/assets/fda14929-61a4-4a2c-af30-6158df4e1b52" />

Execute the following commands in the OpenLane terminal:

```bash
prep -design picorv32a -tag 17-07_09-51 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```

The `prep -design picorv32a -tag 17-07_09-51 -overwrite` command is used to overwrite existing simulation files with previous values.
After synthesis, we observed negative slack values:
WNS (Worst Negative Slack) = -23.89
TNS (Total Negative Slack) = -711.59.

<img width="960" height="919" alt="Screenshot 2025-07-20 213041" src="https://github.com/user-attachments/assets/2577cf84-da93-40c1-8af5-9164de56a228" />

<img width="956" height="1016" alt="Screenshot 2025-07-20 213108" src="https://github.com/user-attachments/assets/b6596902-fe67-4444-943a-47202974b7c9" />

Upon running `run_synthesis` again, we observe an increase in chip area and a reduction in slack.
Since the synthesis of picorv32a is now successful, we will proceed to run floorplan using the command `run_floorplan`.

<img width="953" height="1017" alt="Screenshot 2025-07-20 221054" src="https://github.com/user-attachments/assets/79b22f66-16d7-41d4-8e6b-23418a31a9a5" />

As an error is encountered, we first need to re-run synthesis using the commands mentioned earlier. Subsequently, we will use the following commands for floorplanning:

```bash
init_floorplan
place_io
tap_decap_or
```

<img width="894" height="442" alt="Screenshot 2025-07-20 221306" src="https://github.com/user-attachments/assets/64445b36-7dc4-4ea0-ac95-39e179a46f65" />

<img width="891" height="510" alt="Screenshot 2025-07-20 221316" src="https://github.com/user-attachments/assets/f2e3fb83-a084-4e99-8a22-0268c0bf23fd" />

<img width="895" height="606" alt="Screenshot 2025-07-20 221654" src="https://github.com/user-attachments/assets/08624403-8b78-45fe-b96d-4c1b1f8b7e1b" />

Now, we are ready to execute placement using the command `run_placement`.

<img width="958" height="1017" alt="Screenshot 2025-07-20 221947" src="https://github.com/user-attachments/assets/c9339a28-4a4d-440c-a61c-01c13e57fc50" />

Placement has now completed successfully without any errors.

<img width="952" height="1020" alt="Screenshot 2025-07-20 222423" src="https://github.com/user-attachments/assets/655389ee-dfb6-4a8e-8c50-c20ea8cd1d62" />

<img width="957" height="1018" alt="Screenshot 2025-07-20 222503" src="https://github.com/user-attachments/assets/4cf2076d-aa20-4601-bc99-86473f2590c6" />

We will then run the `expand` command in the tkcon window.

<img width="957" height="1016" alt="Screenshot 2025-07-20 231654" src="https://github.com/user-attachments/assets/d8867242-a682-402a-8e07-c35ab680a009" />

#### Timing analysis with ideal clocks using openSTA

**Setup timing analysis and introduction to flip-flop setup time**
Timing analysis (with ideal clock): Let's begin the setup analysis with an ideal, single clock. The clock specifications are:
* Clock frequency = 1 GHz
* Clock period = 1 ns

We will analyze the timing between the '0' and 'T' clock periods. An edge is sent to the launch flip-flop at time '0', and the second edge reaches the capture flip-flop at time T=1ns.
Assuming a combinational delay of 'theta', setup timing analysis dictates that this combinational delay must be less than 'T' for the system to function correctly.

<img width="998" height="555" alt="Screenshot 2025-07-23 154100" src="https://github.com/user-attachments/assets/03e424fe-dc47-42eb-9bc7-6faf86d5c8d8" />

Next, let's examine the capture flip-flop. It contains various internal components: combinational circuits, MOSFETs, logic gates, resistances, and capacitances. A corresponding time graph for this flip-flop is also available.

<img width="768" height="268" alt="Screenshot 2025-07-20 235716" src="https://github.com/user-attachments/assets/bad187e8-eb74-4db0-95a7-b373e54a5b08" />

When Clock 1 is at logic '0' or '1', the delay of MUX1 and MUX2 will constrain or affect the combinational delay requirement.
Consequently, a finite amount of time is required for the D input to settle. This duration is referred to as SET UP TIME.
Hence, a finite time 'S' is required before the clock edge for the 'D' input to reliably reach Qm.
Thus, the internal delay of MUX1 equals the setup time (S).
The condition θ < T therefore becomes θ < (T - S).

#### Introduction to clock jitter and uncertainty

In the context of Jitter, clocks are typically generated by PLLs (Phase-Locked Loops). Although the clock source is expected to produce signals precisely at 0, T, 2T, etc., it may not always generate them at exact times due to inherent internal variations. This phenomenon is known as jitter, which refers to a temporary variation in the clock pulse.

<img width="763" height="175" alt="Screenshot 2025-07-21 003228" src="https://github.com/user-attachments/assets/36922ec6-8305-4f61-9561-149d9bb6c866" />

Let's incorporate this uncertainty time (US) into our consideration. The equation then becomes θ < (T - S - US). Assuming 'S' = 0.01ns and 'US' = 0.09ns, we can now identify the timing path in our circuit's Stage 1 and Stage 3 logic paths, which utilize a single clock.
Our next step is to identify the combinational path delay for both logic paths.

<img width="805" height="428" alt="Screenshot 2025-07-21 004022" src="https://github.com/user-attachments/assets/238a4f74-837f-45a0-8f2b-a9143bc0704f" />

<img width="739" height="418" alt="Screenshot 2025-07-21 004200" src="https://github.com/user-attachments/assets/aa1297ec-7fd9-42a6-9a67-1d582c6e8f16" />

#### Lab steps to configure OpenSTA for post-synth timing analysis

We need to perform Static Timing Analysis (STA) on the picorv32a design, which previously exhibited timing violations. First, we will run synthesis using the following commands in the OpenLane directory:

```bash
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
run_synthesis
```

<img width="959" height="1015" alt="Screenshot 2025-07-21 011410" src="https://github.com/user-attachments/assets/b27ccb07-5343-4215-85ad-ecfe0179bdf0" />

Now, we must create a new `pre_sta.conf` file. This can be done using a vim editor or any simple text editor.

<img width="951" height="1021" alt="Screenshot 2025-07-21 013427" src="https://github.com/user-attachments/assets/cb611c1d-d899-45c1-a0cb-cc7019655855" />

<img width="952" height="1018" alt="Screenshot 2025-07-21 013437" src="https://github.com/user-attachments/assets/23ffa325-4d57-4a73-8abe-d0a08411c487" />

Next, we will create a `my_base.sdc` file that will contain environment variable definitions.
This `my_base.sdc` file also needs to be created in the `openlane/designs/picorv32a/src` directory, containing the data shown in the image below:

<img width="950" height="1016" alt="Screenshot 2025-07-21 031837" src="https://github.com/user-attachments/assets/876c8ff1-c055-40d8-87af-e63f06ac82b0" />

<img width="957" height="1023" alt="Screenshot 2025-07-21 031916" src="https://github.com/user-attachments/assets/8d342576-86ab-420a-a7fe-2d00aca11a1d" />

Now, navigate to the OpenLane directory in a new terminal and execute the `sta pre_sta.conf` command.

<img width="953" height="1017" alt="Screenshot 2025-07-21 031927" src="https://github.com/user-attachments/assets/c73dfe07-221d-45cc-a766-21341b0f2b05" />

<img width="948" height="1014" alt="Screenshot 2025-07-21 032013" src="https://github.com/user-attachments/assets/7ee81f0d-1814-437b-ab03-536d460b69f1" />

<img width="957" height="1022" alt="Screenshot 2025-07-21 032024" src="https://github.com/user-attachments/assets/e7da34ae-aa95-4072-a0c5-6b4074e6efe5" />

#### Lab steps to optimize synthesis to reduce setup violations

We will now modify the FANOUT parameter and re-run synthesis with the following commands:

```bash
prep -design picorv32a -tag 17-07_09-51 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_SIZING) 1
set ::env(SYNTH_MAX_FANOUT) 4
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```
<img width="959" height="1015" alt="Screenshot 2025-07-21 035026" src="https://github.com/user-attachments/assets/8b3c7b92-aeef-4122-abf8-635587aed045" />

<img width="957" height="1015" alt="Screenshot 2025-07-21 035123" src="https://github.com/user-attachments/assets/ef70d5b0-44c4-4757-94ad-e5a7cca36d6f" />

Now, execute the `sta pre_sta.conf` command in a new terminal within the OpenLane directory itself.

<img width="956" height="1015" alt="Screenshot 2025-07-21 035228" src="https://github.com/user-attachments/assets/1d084cd8-8b94-4e4e-b217-02efc914df2d" />

<img width="956" height="1014" alt="Screenshot 2025-07-21 035307" src="https://github.com/user-attachments/assets/4455efd7-e0eb-40bf-bd02-95e5edd3a694" />

#### Lab steps to do basic timing ECO

Consider an OR gate with a drive strength of 2, driving a fanout of 4.

<img width="888" height="196" alt="Screenshot 2025-07-21 100257" src="https://github.com/user-attachments/assets/11ce790e-5a1c-4587-a8c6-fe6a93aa11ae" />

To address this, we need to replace this OR gate with another OR gate having a drive strength of 4. Execute the following commands:
To report all connections to a net:

```bash
report_net -connections _11672_
```

To check command syntax:

```bash
help replace_cell
```

To replace the cell:

```bash
replace_cell _14510_ sky130_fd_sc_hd__or3_4
```

To generate the custom timing report:

```bash
report_checks -fields {net cap slew input_pins} -digits 4
```

<img width="955" height="1019" alt="Screenshot 2025-07-21 101031" src="https://github.com/user-attachments/assets/f3504748-84cb-4093-92d0-bb05cba04269" />

<img width="961" height="1017" alt="Screenshot 2025-07-21 101052" src="https://github.com/user-attachments/assets/fbbadfcb-4b26-4632-a6f4-f1aaf6718e54" />

We can observe that the slack has reduced from -23.89 to -23.51.

<img width="892" height="198" alt="Screenshot 2025-07-21 101216" src="https://github.com/user-attachments/assets/9c8d30a1-9e56-4017-aae4-8bc5402ab478" />

In the case above, another OR gate with a drive strength of 2 is also driving a fanout of 4.
We must replace this OR gate with another OR gate having a drive strength of 4 by following these commands:
To report all connections to a net:

```bash
report_net -connections _11675_
```

To replace the cell:

```bash
replace_cell _14514_ sky130_fd_sc_hd__or3_4
```

To generate the custom timing report:

```bash
report_checks -fields {net cap slew input_pins} -digits 4
```

#### Clock tree synthesis TritonCTS and signal integrity

**Clock tree routing and buffering using H-Tree algorithm**
**Clock tree synthesis:** This involves physically connecting clk1 to sequential elements like FF1 & FF2 of Stage 1, and FF1 of Stage 3 & FF2 of Stage 4.

<img width="879" height="430" alt="Screenshot 2025-07-21 120257" src="https://github.com/user-attachments/assets/bba38ba7-0ce7-42af-9353-3eb8a4e79cac" />

Now, let's identify a potential problem. If there's a physical distance between the clock source and FF1, and FF2, it could lead to t2 > t1.
Skew is defined as t2 - t1, and ideally, it should be 0ps.

<img width="481" height="173" alt="Screenshot 2025-07-21 124238" src="https://github.com/user-attachments/assets/77211115-5f9c-4ed3-bb8e-eb7445e7d449" />

Previously, we built a non-optimal clock tree. We will now optimize it. By routing the clock to arrive at midpoints, it can reach every flip-flop at almost the same time. Similarly, clk2 will be connected to its flip-flops in a midpoint manner.

<img width="898" height="426" alt="Screenshot 2025-07-21 124514" src="https://github.com/user-attachments/assets/73ea7df6-ed5e-4548-8aae-b0f3319db077" />

Next, we will examine clock tree synthesis (Buffering). When a clock signal travels along a route to specific locations and clock endpoints, it encounters various capacitances and resistors along the path.

<img width="614" height="339" alt="Screenshot 2025-07-21 125524" src="https://github.com/user-attachments/assets/d2ddef44-12c7-4c6b-8b45-14899926c2cf" />

Due to wire length and RC networks, the output waveform may not be identical to the input. To resolve this, repeaters are used. The key difference for clock repeaters, compared to data path repeaters, is that they ensure equal rise and fall times.
The first step involves removing the existing clock route and placing two repeaters, allowing the clock to pass through them. In this scenario, the waveform generated by the repeaters will be propagated to the output. We can insert as many repeaters as needed to maintain a continuous flow of the clock signal to the output.

<img width="895" height="441" alt="Screenshot 2025-07-21 130016" src="https://github.com/user-attachments/assets/54f9135a-f365-43c5-aa78-bff55e5b7722" />

**Crosstalk and clock net shielding**
**Clock Net Shielding:** Our objective is to design the clock tree such that the skew between the launch flip-flop and capture flip-flop is 0. Skew refers to the latency difference between the clock ports of the flip-flop pins. Clock net shielding is a critical aspect in design. We essentially "shield" a particular clock net, protecting it from external interference, much like providing a "house" for the clock.

<img width="605" height="433" alt="Screenshot 2025-07-21 130606" src="https://github.com/user-attachments/assets/c4e0493a-b413-4131-a03b-db35b69b07a2" />

If the clock net is left unprotected, two common problems can arise: Glitch and Delta Delay.
Consider a clock net. When switching activity occurs on a nearby "aggressor" net, the strong coupling capacitance between the wires can directly impact the adjacent "victim" net.

<img width="427" height="224" alt="Screenshot 2025-07-21 130908" src="https://github.com/user-attachments/assets/1210529c-3dd7-46bf-926c-668619f224cd" />

Shielding is a technique that protects the victim net from these issues. In shielding, a wire is placed between the two wires where coupling capacitance is generated. This extra wire is then either grounded or connected to VDD.
We observe that a delta delay occurs due to a "bump" when the signal switches from logic '1' to '0'. Consequently, the skew is no longer zero. The impact of crosstalk-induced delta delay is that it introduces a non-zero skew value.

<img width="849" height="478" alt="Screenshot 2025-07-21 131109" src="https://github.com/user-attachments/assets/5c1254f1-5b87-4674-8e67-0781169a742d" />

By implementing shielding, we effectively break the coupling capacitance between the aggressor and victim nets. Shields are designed not to switch, further enhancing isolation.

#### Lab steps to run CTS using Triton

We now need to replace the old netlist with the newly generated netlist (which resulted from slack reduction). Following this, we will run floorplan, placement, and Clock Tree Synthesis (CTS).

<img width="956" height="1015" alt="Screenshot 2025-07-21 134805" src="https://github.com/user-attachments/assets/a8f8b214-b87f-4fca-a1d8-a36da3a3b6db" />

The image above shows the netlist before the modifications were made.
To proceed, we must create a copy of this old netlist and then introduce the newly generated netlist into our OpenLane flow for subsequent processing.
Create the copy using the following commands:
To go to the specified location:

```bash
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-07_09-5127/results/synthesis/
```

To list the contents:

```bash
ls -ltr
```

To copy the netlist with a specific name:

```bash
cp picorv32a.synthesis.v picorv32a.synthesis_old.v
```

To list the contents again:

```bash
ls -ltr
```

<img width="957" height="1014" alt="Screenshot 2025-07-21 135413" src="https://github.com/user-attachments/assets/79349f74-0169-4c54-b5b6-f7ddbe5eaa29" />

Now, we will re-run synthesis, then floorplan, placement, and CTS directly in the OpenLane directory using the following commands:

```bash
prep -design picorv32a -tag 17-07_09-51 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
set ::env(SYNTH_STRATEGY) "DELAY 3"
set ::env(SYNTH_SIZING) 1
run_synthesis
init_floorplan
place_io
tap_decap_or
run_placement
# In case getting error will use this command
unset ::env(LIB_CTS)

run_cts
```

<img width="960" height="1019" alt="Screenshot 2025-07-21 142031" src="https://github.com/user-attachments/assets/ba365287-1098-416c-a00c-a865090efd0d" />

<img width="959" height="1016" alt="Screenshot 2025-07-21 142105" src="https://github.com/user-attachments/assets/098a1227-0f52-4c6d-b293-0af038757145" />

A `.cts` file has now been created in the specified location, as shown in the image above.

<img width="958" height="1018" alt="Screenshot 2025-07-21 142132" src="https://github.com/user-attachments/assets/6dd8e684-ee0f-44da-8a3a-c63dc694f7d7" />

#### Lab steps to verify CTS runs

**OPENROAD:** To create a database in OPENROAD using LEF and TMP files, use the following commands:
First, ensure you are in the directory containing the LEF and TMP files.
Then, enter the following command to start the OPENROAD tool:

```bash
openroad
```

Once inside the OPENROAD tool, enter the following commands to create the database:
To read the LEF file:

```bash
read_lef /openLANE_flow/designs/picorv32a/runs/17-07_09-51/tmp/merged.lef
```

To read the DEF file:

```bash
read_def /openLANE_flow/designs/picorv32a/runs/17-07_09-51/results/cts/picorv32a.cts.def
```

To create an OpenROAD database file named pico_cts.db:

```bash
write_db pico_cts.db
```

You can now observe that this database file is present in the OpenLane directory.

#### Timing analysis with real clock using openSTA

**Setup timing analysis using real clocks**
With a real clock, the circuit tree differs slightly from an ideal clock scenario, as it includes buffers and wires. The clock signal does not reach the launch or capture flip-flop at exactly t=0 due to delays introduced by these buffers.
The combinational circuit equation, initially θ < T for an ideal clock, becomes (θ + Δ1) < (T + Δ2).

<img width="829" height="481" alt="Screenshot 2025-07-21 152442" src="https://github.com/user-attachments/assets/241a800a-4df8-4df1-92d1-855b76331a65" />

Let's define Δ1 as (1 + 2) and Δ2 as (1 + 3 + 4). The skew is then (Δ1 - Δ2).

<img width="844" height="463" alt="Screenshot 2025-07-21 152945" src="https://github.com/user-attachments/assets/140291fa-2bdb-47c2-98a0-38615580ff84" />

Furthermore, we must account for propagation skew (S) and uncertainty delay (US). The final equation then transforms to (θ + Δ1) < (T + Δ2 - S - US).
We can also define (θ + Δ1) as the data arrival time and (T + Δ2 - S - US) as the data required time.
If (Data required time) - (Data arrival time) is positive, the timing is acceptable. If it is negative, it indicates 'slack' (a timing violation).

**Hold timing analysis**
Hold timing analysis is distinct from setup timing analysis. Here, we consider the first clock pulse simultaneously reaching both the launch flip-flop and the capture flip-flop.
The Hold condition states that the Hold time (H) must be less than the combinational delay (θ), or (θ > H).

<img width="857" height="486" alt="Screenshot 2025-07-21 153406" src="https://github.com/user-attachments/assets/1a2c5159-6553-4196-ac31-995cbb3dbfc8" />

Hence, a finite time 'H' is required for Qm to reliably reach Q; this internal delay of MUX2 is equivalent to the hold time.
When incorporating a real-time clock, the equation changes to (θ + Δ1) > (H + Δ2).

<img width="773" height="441" alt="Screenshot 2025-07-21 154007" src="https://github.com/user-attachments/assets/9c2301c7-3637-44b6-bc95-fbeeeb50bcb2" />

**Hold timing analysis using real clocks**
The combinational delay should be greater than the hold time of the capture flip-flop.
Once the clock reaches the launch flip-flop, it incurs approximately two buffer delays (Δ1). When it reaches the capture flip-flop, it incurs about three buffer delays (Δ2). The uncertainty value remains consistent for both flip-flops because the clock is applied from the same edge. Now, let's add the uncertainty value.

<img width="721" height="416" alt="Screenshot 2025-07-21 154853" src="https://github.com/user-attachments/assets/98390f9d-4875-4451-93aa-70d50918ad22" />

Slack is calculated as Data arrival time - data required time. Slack should ideally be positive or zero. If slack becomes negative, it signifies a violation.

<img width="786" height="144" alt="Screenshot 2025-07-21 154913" src="https://github.com/user-attachments/assets/fb689fe6-1319-4d66-9680-c3edcf90d022" />

Let's identify the timing paths from the design, assuming a single clock.

<img width="826" height="443" alt="Screenshot 2025-07-21 155522" src="https://github.com/user-attachments/assets/866e5c03-0dfb-4c71-9ef8-d47ca75be760" />

<img width="304" height="71" alt="Screenshot 2025-07-21 155622" src="https://github.com/user-attachments/assets/8e9917f5-67fb-47b7-98b1-0d4ece43b4ef" />
<img width="221" height="75" alt="Screenshot 2025-07-21 155642" src="https://github.com/user-attachments/assets/700e7f31-d8ab-4890-b9f2-380fb4ab2ef3" />


#### Lab steps to analyze timing with real clocks using OpenSTA

Now, execute the following commands:
To load the created database file in OpenROAD:

```bash
read_db pico_cts.db
```

To read the netlist post-CTS:

```bash
read_verilog /openLANE_flow/designs/picorv32a/runs/17-07_09-51/results/synthesis/picorv32a.synthesis_cts.v
```

To read the library for the design:

```bash
read_liberty $::env(LIB_SYNTH_COMPLETE)
```

To link the design and library:

```bash
link_design picorv32a
```

To read the custom SDC file we created:

```bash
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
```

To set all clocks as propagated clocks:

```bash
set_propagated_clock [all_clocks]
```

To generate the custom timing report:

```bash
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```

To exit from OpenLane flow:

```bash
exit
```

<img width="958" height="1015" alt="Screenshot 2025-07-21 164242" src="https://github.com/user-attachments/assets/b57cef5a-f648-4fbd-b910-ad184935bbd2" />

<img width="955" height="1018" alt="Screenshot 2025-07-21 164705" src="https://github.com/user-attachments/assets/356dd5ca-fc93-46f7-b558-97219d548c17" />

<img width="960" height="1032" alt="Screenshot 2025-07-21 164726" src="https://github.com/user-attachments/assets/e39297dc-6317-46b5-81ec-776ee118d3c4" />

#### Lab steps to execute OpenSTA with right timing libraries and CTS assignment

To remove `sky130_fd_sc_hd__clkbuf_1` from the list:

```bash
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
```

To check the current value of `CTS_CLK_BUFFER_LIST`:

```bash
echo $::env(CTS_CLK_BUFFER_LIST)
```

To check the current value of `CURRENT_DEF`:

```bash
echo $::env(CURRENT_DEF)
```

To set the DEF as placement DEF:

```bash
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/17-07_09-51/results/placement/picorv32a.placement.def
```

To run CTS:

```bash
run_cts
```

To check the current value of `CTS_CLK_BUFFER_LIST`:

```bash
echo $::env(CTS_CLK_BUFFER_LIST)
```

#### Lab steps to observe impact of bigger CTS buffers on setup and hold timing

Now, we will follow the same commands used earlier to run OPENROAD:

```bash
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/17-07_09-51/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/17-07_09-51/results/cts/picorv32a.cts.def
write_db pico_cts1.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/17-07_09-51/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
report_clock_skew -hold
report_clock_skew -setup
exit
```
<img width="957" height="1018" alt="Screenshot 2025-07-21 181418" src="https://github.com/user-attachments/assets/ab2a4490-b3ad-41f6-8bd0-afc695366a62" />

<img width="958" height="1021" alt="Screenshot 2025-07-21 181527" src="https://github.com/user-attachments/assets/8284c1e6-6671-4d7c-8ac7-a8a9d114fc2f" />

<img width="955" height="980" alt="Screenshot 2025-07-21 182248" src="https://github.com/user-attachments/assets/f817c134-b52e-445e-ba9d-802bf6b0ae98" />

<img width="958" height="1015" alt="Screenshot 2025-07-21 184936" src="https://github.com/user-attachments/assets/4cf7530a-f4aa-4123-b20f-f6dc95bca1a9" />

---

### Day 5 - Final step for RTL2GDS using tritinRoute and openSTA

#### Routing and design rule check (DRC)

The next and final stage in physical design involves Routing and Design Rule Check (DRC).
**Routing:** This process identifies the shortest and most efficient connection path between two endpoints (a source and a target), minimizing unnecessary twists and turns.

#### Introduction to Maze Routing - Lee's algorithm

**Maze-Routing (Lee's Algorithm):** There should not be zig-zag lines of connections; most connections should be in an L-shape or Z-shape. The algorithm begins by creating a grid system, known as a routing grid, which is used for backend routing. This grid consists of cells with defined dimensions.
Given a 'Source' point and a 'Target' point, the algorithm utilizes this routing grid to determine the optimal path between them.
The first step of the algorithm is to label all surrounding grid cells. Only horizontally and vertically adjacent grids are labeled; diagonal ones are excluded, as illustrated in the image below.

<img width="498" height="415" alt="Screenshot 2025-07-21 195944" src="https://github.com/user-attachments/assets/c4c03ea3-014c-4e35-bd35-f3363efe183d" />


#### Lee's Algorithm conclusion

Now, we label the grids sequentially with integers until the target is reached. In the example, the target was reached after integer 9.

<img width="495" height="411" alt="Screenshot 2025-07-21 200548" src="https://github.com/user-attachments/assets/60b87dfd-8e69-49d3-acc7-738b21a75cb8" />


Although numerous paths can lead from the source to the target, we must select the shortest and most optimal route. It's crucial to avoid zig-zag paths; 'L'-shaped routing is generally preferred.

<img width="497" height="409" alt="Screenshot 2025-07-21 200627" src="https://github.com/user-attachments/assets/94816f00-a596-4e02-a255-41efe8a2e22a" />

Let's consider another example for routing, following the exact same steps as detailed above.

<img width="500" height="411" alt="Screenshot 2025-07-21 200930" src="https://github.com/user-attachments/assets/d640266e-bdef-437c-8862-b13b2c62fba7" />

<img width="612" height="438" alt="Screenshot 2025-07-21 201038" src="https://github.com/user-attachments/assets/b1014afe-07ea-4115-97ef-8f9ff01b34f2" />


#### Design Rule Check

To perform a Design Rule Check (DRC), we follow specific steps known as DRC cleaning.
Consider the example of the circuit shown above. If we have two parallel wires, a fundamental rule dictates that there must be a minimum separation distance between them.

<img width="609" height="423" alt="Screenshot 2025-07-21 201515" src="https://github.com/user-attachments/assets/1f256ba2-73ba-4965-8722-5e625bacf347" />


* **Rule 1) Wire Width:** The wire's width must adhere to a minimum value, which is derived from the optical wavelength of the lithography technique applied during fabrication.

<img width="257" height="129" alt="Screenshot 2025-07-21 201600" src="https://github.com/user-attachments/assets/8af1aa20-b235-4ab6-8037-c78e40c6855f" />

* **Rule 2) Wire Pitch:** The minimum pitch between two wires should be as specified in the figure below.

<img width="278" height="134" alt="Screenshot 2025-07-21 201840" src="https://github.com/user-attachments/assets/a8fa0444-17d6-45b0-bbab-4236e0a57f3d" />


* **Rule 3) Wire Spacing:** The spacing between two wires should conform to the dimensions shown in the image below.

<img width="266" height="150" alt="Screenshot 2025-07-21 201931" src="https://github.com/user-attachments/assets/264b1978-151d-4f0b-bf3a-2b05ca07b2d3" />

Let's examine another aspect of design rule checking using the same example.

<img width="881" height="441" alt="Screenshot 2025-07-21 202032" src="https://github.com/user-attachments/assets/0abeac48-7d42-448b-856e-25bc69bdf054" />

The solution to a signal short problem often involves placing one of the wires on a different metal layer. Typically, upper metal layers are wider than lower ones.

<img width="223" height="206" alt="Screenshot 2025-07-21 202253" src="https://github.com/user-attachments/assets/f032252d-7eb7-44af-986d-ea84c06ec6aa" />

After implementing this solution, two new DRC rules must be verified:

* **Rule 1) Via Width:** The via width should be set to a minimum specified value.

<img width="219" height="193" alt="Screenshot 2025-07-21 202339" src="https://github.com/user-attachments/assets/e663be81-c105-45f2-8c35-fd418b5b541f" />

* **Rule 2) Via Spacing:** The spacing between vias should also meet a minimum value.

<img width="211" height="196" alt="Screenshot 2025-07-21 202534" src="https://github.com/user-attachments/assets/5f117d1f-5a17-46dd-b227-749422b87abc" />

Following routing and DRC, the next crucial step is Parasitic Extraction. The resistance and capacitance inherent in every wire must be extracted and utilized for subsequent processes.

<img width="601" height="446" alt="Screenshot 2025-07-21 202651" src="https://github.com/user-attachments/assets/dd954df7-bd22-4df5-a5b4-6374fb5782f0" />

#### Power Distribution Network and routing

#### Lab steps to build power distribution network

Commands executed in the previous terminal session are provided below:

```bash
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag 17-07_09-51
echo $::env(CURRENT_DEF)
```

At this point, Clock Tree Synthesis (CTS) has been completed. Now, we prepare for routing. Before routing, we must generate the Power Distribution Network (PDN) file using the command:

```bash
gen_pdn
```

<img width="952" height="1015" alt="Screenshot 2025-07-21 203346" src="https://github.com/user-attachments/assets/94400825-8ed9-40b2-a45d-af257bd39fd1" />
<img width="960" height="1015" alt="Screenshot 2025-07-21 203420" src="https://github.com/user-attachments/assets/6d6a08fc-5772-463d-8e2e-629cedccd57b" />


The output indicates that the net VGND displays the total number of nodes on the grid matrix, confirming successful creation of the PDN.
Power is delivered to the chip through VDD and GND pads. This power then travels through tracks, ultimately reaching and powering the individual cells.

#### Lab steps from power straps to std cell power

<img width="501" height="331" alt="Screenshot 2025-07-21 204110" src="https://github.com/user-attachments/assets/21b34795-b98a-4455-a954-307c12160ebc" />


In the image above, green represents the chip, while yellow, red, and blue boxes denote I/O pins, power pads, and ground pads, respectively.
Power is transferred from the pads to the power rings via black dots visible at the cross-section points of the ring and pads.
Vertical and horizontal tracks ensure that power is efficiently transferred from the power rings to the chip, as indicated by the red and blue coloring. This illustrates how power planning is executed in the physical design of any device.

#### Basics of global and detail routing and configure TritonRoute

The final stage of physical design is Routing.

<img width="957" height="1018" alt="Screenshot 2025-07-21 205322" src="https://github.com/user-attachments/assets/238c1b32-9c41-4496-b04b-fd71473a0367" />

The `def` command usage shown in the image indicates that the most recently completed step was the generation of the PDN.
The resulting `17-pdn.def` file contains information from `cts.def` as well as the newly generated power distribution network details.
For information regarding the various switches available for routing, users can refer to the `README.md` file located in the configuration folder within the OpenLANE directory.

<img width="958" height="1017" alt="Screenshot 2025-07-21 205532" src="https://github.com/user-attachments/assets/878bac97-4c2a-4569-ae32-532bfd0f141b" />

By executing specific commands, the type of global and detailed routing to be performed can be determined.
Should a change in routing type be desired, the `set` command can be used, followed by the relevant parameter names found in the routing section of the `README.md` file.
In this specific instance, however, the default routing types have been utilized.

<img width="813" height="100" alt="Screenshot 2025-07-21 205811" src="https://github.com/user-attachments/assets/d54428f9-389a-4f84-b0a3-ff8c201853a1" />

Now, we will initiate the routing process using the command:

```bash
run_routing
```
<img width="959" height="1019" alt="Screenshot 2025-07-21 211516" src="https://github.com/user-attachments/assets/e9d21017-6371-4f1e-8e00-c5e61814870c" />

The entire routing process is divided into two main parts:
* Fast route (Global route)
* Detailed Route

<img width="814" height="359" alt="Screenshot 2025-07-21 211549" src="https://github.com/user-attachments/assets/a32d84d3-880c-4258-8c2e-55a22e53578b" />

In the Global route, the routing region is divided into rectangular grid cells, as shown in the figure above. This is represented as a 3D routing graph of the core. Global routing is handled by the FAST route engine.
The Detailed route is performed by the TritonRoute engine. A, B, C, and D are four pins intended for connection via routing, and this entire illustration (A, B, C, D) represents a net.

#### TritonRoute Features

**TritonRoute feature 1 - Honors pre-processed route guides**
TritonRoute performs initial detailed routing.
It honors the preprocessed route guides, which are obtained after the fast routing stage.

<img width="624" height="195" alt="Screenshot 2025-07-21 223348" src="https://github.com/user-attachments/assets/be6fa708-d011-45ac-988d-2ab9a5ff1986" />

Requirements of preprocessed guides:
* Should have unit width.
* Should be in the preferred direction.
* Assumes route guides for each net satisfy inter-guide connectivity.

Two guides are considered connected if:
* They are on the same metal layer with touching edges.
* They are on neighboring metal layers with a non-zero vertically overlapped area.

TritonRoute operates based on a proposed MILP (Mixed-Integer Linear Programming)-based panel-routing scheme, incorporating an intra-layer parallel and inter-layer sequential routing framework.

**TritonRoute Feature2 & 3 - Inter-guide connectivity and intra- & inter-layer routing**
Each unconnected terminal (i.e., pin of a standard-cell instance) should have its pin shape overlapped by a route guide.

<img width="298" height="153" alt="Screenshot 2025-07-21 224047" src="https://github.com/user-attachments/assets/fbc25061-1cb8-4866-a43c-ba98207744ac" />

As seen here, the black dots representing cell pins are overlapped by the route guides. If pins are located at the intersection of vertical and horizontal tracks, this ensures they will be overlapped by route guides.

**Intra-layer parallel and inter-layer sequential panel routing:**
* Intra-layer refers to routing within the same metal layer.
* Inter-layer refers to routing between different metal layers.

<img width="583" height="176" alt="Screenshot 2025-07-21 224327" src="https://github.com/user-attachments/assets/4821b441-2384-46f8-8faf-a66e98521d0c" />

In this figure, we can observe 4 layers of metal. Each of these layers is divided into segments marked by "--" lines. Focusing on Metal 2 layer, where we assume a vertical routing direction, these "--" lines are called panels. Each panel is assigned routing guides. The blue arrows indicate that routing happens in the even-indexed panels, signifying intra-layer parallel routing. First, it occurs in even-indexed panels, then in odd-indexed panels, all in parallel within that particular layer.

<img width="661" height="222" alt="Screenshot 2025-07-21 224551" src="https://github.com/user-attachments/assets/e80b5ac0-0fc5-48e9-924b-4c6c4b62c947" />

(a) figure shows the parallel routing of panels on M2.
(b) figure, we can see the parallel routing of even panels on M3.
(c) figure shows the parallel routing of odd panels on M3.

#### TritonRoute method to handle connectivity

* **INPUTS:** LEF
* **OUTPUTS:** Detailed routing solution with optimized wire-length and via count
* **CONSTRAINTS:** Route guide honoring, connectivity constraints, and design rules

Now, we need to define the space where detailed routing takes place.

**Handling Connectivity**

<img width="547" height="176" alt="Screenshot 2025-07-21 224928" src="https://github.com/user-attachments/assets/45f4059e-5ff0-4b34-8f27-fdfa304068d5" />

* **Access Point (AP):** An on-grid point on the metal layer of the route guide, used to connect to lower-layer segments, upper-layer segments, pins, or I/O ports.
* **Access Point Cluster (APC):** A union of all access points derived from the same lower-layer segment, upper-layer guide, a pin, or an I/O port.

The figure below illustrates access points:
* (a) To a lower-layer segment
* (b) To a pin shape
* (c) To an upper layer

#### Routing topology algorithm and final files list post-route

<img width="387" height="199" alt="Screenshot 2025-07-21 230011" src="https://github.com/user-attachments/assets/1e18eb57-ac21-4a35-bc61-42c467be4227" />

The algorithm requires determining the cost associated with each Access Point Cluster (APC) and calculating the minimum spanning tree between APCs to find the optimal connections.
The subsequent step involves post-routing Static Timing Analysis (STA), which necessitates the extraction of parasitic effects (SPEF).
As OpenLANE currently lacks a built-in SPEF extraction tool, this process must be performed externally.
The resulting `.spef` file can be found in the routing folder, located under the results folder.

<img width="887" height="571" alt="Screenshot 2025-07-21 231029" src="https://github.com/user-attachments/assets/aca67f4a-7c46-4d40-9180-9490510fcfea" />

<img width="960" height="1017" alt="Screenshot 2025-07-21 231054" src="https://github.com/user-attachments/assets/0a1d3c9e-530a-496f-8303-c7fc63f636a6" />

<img width="880" height="100" alt="Screenshot 2025-07-21 232151" src="https://github.com/user-attachments/assets/adfa5bce-e15d-477f-adce-9f464f6f7390" />

This is the final generated layout.

<img width="957" height="1012" alt="Screenshot 2025-07-21 232513" src="https://github.com/user-attachments/assets/3c195f09-6c20-4576-8962-defa5f63c088" /><img width="953" height="1017" alt="Screenshot 2025-07-21 232548" src="https://github.com/user-attachments/assets/f50a652d-9a16-45dd-8428-ed800d3c21c9" />


---

#### References

* [SkyWater Open Source PDK by Google](https://github.com/google/skywater-pdk)
* [VSD Standard Cell Design GitHub Repository](https://github.com/nickson-jose/vsdstdcelldesign)
* [Ngspice Project on SourceForge](https://sourceforge.net/projects/ngspice/)
* [GitHub – Open-source collaboration platform](https://github.com/)
* [Introduction to Industrial Physical Design Flow (PDF)](https://www.vlsisystemdesign.com/wp-content/uploads/2017/07/Introduction-to-Industrial-Physical-Design-Flow.pdf)

---

#### Acknowledgement

* I would like to extend my heartfelt gratitude to **Mr. Kunal Ghosh**, Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd., and **Mr. Nickson Jose** for their exceptional mentorship and detailed presentation during the **DIGITAL-VLSI-SOC-DESIGN-AND-PLANNING** workshop.
* Their expertise and hands-on guidance played a pivotal role in enhancing my understanding of digital VLSI system design and physical chip design using the OpenLANE toolchain and Sky130 PDK. The workshop was meticulously curated, blending theoretical concepts with practical experience, and has significantly broadened my perspective in the field of ASIC design.
* I am deeply thankful for their unwavering commitment to empowering students and professionals through open-source EDA tools and industry-aligned training.
