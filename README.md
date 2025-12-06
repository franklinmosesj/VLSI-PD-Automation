# VLSI-PD-Automation
This repository contains a complete Physical Design (PD) automation flow for Synopsys ICC2 / Fusion Compiler using TCL scripting.
The flow covers all major stages from netlist import to final routing, implemented in a modular way for easy execution, debugging, and reuse.

Overview

The goal of this project is to provide a step-by-step automated PD flow that can be used by:

VLSI students

Freshers preparing for PD roles

R&D engineers

Anyone learning ICC2 flow scripting

Each stage is separated into individual scripts so you can run, stop, and analyze any step independently.

Flow Stages

The complete implementation flow is structured into eight scripts:

Stage	Description	Script
1️⃣ Import	Library creation, netlist load	import.tcl
2️⃣ Floorplan	Core layout, macro placement	floorplan.tcl
3️⃣ PG Routing	Power grid generation	pg_routing.tcl
4️⃣ Pre-Place	Tap cells, end caps, IO buffers	preplace.tcl
5️⃣ Placement	Standard cell placement	place.tcl
6️⃣ CTS	Clock Tree Synthesis	cts.tcl
7️⃣ Post-CTS	Timing optimization	post_cts.tcl
8️⃣ Routing	Global & detailed routing	route.tcl
Flow Logic

The flow is built on these design principles:

✔ Modular Scripts

Each stage is a separate .tcl file to allow controlled execution.

✔ Database Copying

Each step copies the previous block:

import → floorplan → pg_routing → preplace → place → cts → post_cts → route

✔ User & Tech Setup

All tech/user configs are centralized:

source ./scripts/tech_setup.tcl
source ./scripts/user_setup.tcl

✔ Stop Flags

Every file supports stop variables to pause the flow after a stage.

⚙️ Running the Flow

To execute the entire PD flow:

icc_shell -f import.tcl       | tee logs/import.log
icc_shell -f floorplan.tcl    | tee logs/floorplan.log
icc_shell -f pg_routing.tcl   | tee logs/pg_routing.log
icc_shell -f preplace.tcl     | tee logs/preplace.log
icc_shell -f place.tcl        | tee logs/place.log
icc_shell -f cts.tcl          | tee logs/cts.log
icc_shell -f post_cts.tcl     | tee logs/post_cts.log
icc_shell -f route.tcl        | tee logs/route.log


You can run individual stages if required, e.g.:

icc_shell -f place.tcl

Directory Structure
VLSI-PD-Automation/
├── README.md
├── import.tcl
├── floorplan.tcl
├── pg_routing.tcl
├── preplace.tcl
├── place.tcl
├── cts.tcl
├── post_cts.tcl
└── route.tcl


(Optional: Add logs/, reports/, scripts/ folders)

Requirements

Synopsys ICC2 / Fusion Compiler

Liberty files (*.lib)

Technology files (*.tf, *.ndm)

Verilog netlist

SDC constraints

Linux environment

Author

Franklin Moses
VLSI Physical Design Engineer
Specialized in ASIC implementation, ICC2 flow scripting, and PD automation.
