# NanoRISC-V C2
### RISC-V Processor Design Using Verilog HDL

## Overview

NanoRISC-V C2 is a digital hardware design project focused on implementing a RISC-V-based processor using Verilog HDL. The project explores processor architecture, instruction execution, arithmetic and logic operations, memory interfacing, and control flow.

The design is developed and analyzed using AMD/Xilinx Vivado, with simulation and implementation reports used to study its functionality and hardware characteristics.

## Processor Architecture

NanoRISC-V C2 follows a two-stage processor organization consisting of **Fetch & Decode** and **Execute & Writeback** stages. The design integrates instruction fetching, instruction decoding, immediate generation, register-file access, arithmetic and logic operations, memory access, and program-counter control.

The block diagram below illustrates the major processor components and their interconnections.



![NanoRISC-V C2 Processor Block Diagram](docs/nanoriscv_architecture.png)


## Objectives

- Understand the fundamentals of RISC-V processor architecture.
- Implement processor components using Verilog HDL.
- Design arithmetic, logic, memory, and control-flow operations.
- Use simulation testbenches to examine individual modules and processor behavior.
- Analyze FPGA synthesis and timing reports.
- Gain practical experience with digital design and FPGA development tools.

## Instruction Support

The current control logic includes support for the following instruction operations:

| Category | Instructions |
|---|---|
| Arithmetic and Logic | `ADD`, `SUB`, `AND`, `OR`, `XOR`, `SLL`, `SRL` |
| Immediate Operations | `ADDI` |
| Memory Operations | `LW`, `SW` |
| Conditional Branches | `BEQ`, `BNE` |
| Jump | `JAL` |
| Upper Immediate | `LUI` |

## Tools and Technologies

- **Hardware Description Language:** Verilog HDL
- **Design and Simulation:** AMD/Xilinx Vivado
- **Target FPGA Device in the archived project reports:** `xc7k70tfbv676-1`
- **Timing Constraints:** XDC

## Simulation and Verification

The project includes module-level testbenches for major processor components, along with a top-level testbench for examining processor behavior.

Simulation can be used to study:

- Arithmetic and logical operations.
- Instruction decoding and control-signal generation.
- Immediate-value generation.
- Register-file operations.
- Instruction and data-memory behavior.
- Program-counter updates and processor execution.

### Verification Status
| Testbench | Module Tested | Verification Result |
|---|---|---|
| `tb_alu` | `alu` | **PASS (verified)** |
| `tb_control_unit` | `control_unit` | **PASS** |
| `tb_dmem` | `dmem` | **PASS (saved xsim log)** |
| `tb_if_id_reg` | `if_id_reg` | **PASS (waveform verified)** |
| `tb_imem` | `imem` | **PASS** |
| `tb_imm_gen` | `imm_gen` | **PASS** |
| `tb_pc_reg` | `pc_reg` | **PASS** |
| `tb_regfile` | `regfile` | **PASS** |
| `tb_nanoriscv_top` | `nanoriscv_top` | **PASS (Integration Test Successful)** |

## Synthesis and Timing Analysis

The archived Vivado implementation reports contain the following results for the selected FPGA target:

| Parameter | Result |
|---|---:|
| Slice LUTs | 495 |
| Slice Registers | 128 |
| RAMB18 Blocks | 3 |
| DSP Blocks | 0 |
| Clock Period Constraint | 20 ns |
| Routed Worst Negative Slack (WNS) | +8.731 ns |
| Routed Total Negative Slack (TNS) | 0 ns |

The archived routed timing report indicates that the design met the specified timing constraints for that implementation run. Results may vary if the RTL, constraints, target device, or tool settings change.

## Machine Learning Stall Analysis & Telemetry

To evaluate pipeline efficiency, a 500-row execution trace dataset (`dataset.csv`) was analyzed using Python.

### Random Forest Classifier Results
- **Model:** Random Forest Classifier (`random_state=42`, `test_size=0.2`)
- **Features:** Opcode (one-hot encoded), source registers (`rs1`, `rs2`), and destination register (`rd`)
- **Target:** Pipeline stall prediction (`stall`)
- **Test Accuracy:** **87.00%** (Matches majority-class baseline)

### Telemetry Insights
- **Stall Rates & CPI:** The mean Cycles Per Instruction (CPI) across the trace is 1.688. Instructions like `ADD` (13.8%), `SW` (13.5%), and `LW` (10.7%) exhibit higher stall frequencies.
- **Branch Outcomes:** `BEQ` instructions have a taken rate of 23.1%, resulting in control flow redirects that flush the pipeline and cost cycles.

## Multi-Model AI Disclosure

In accordance with academic integrity and ethical guidelines, multiple AI assistants collaboratively contributed to this project:
- **ChatGPT (OpenAI):** Initial RTL code structuring and instruction-set architecture (ISA) debugging.
- **Claude (Anthropic):** Synopsis drafting, dataset structuring, and Vivado report analysis.
- **Gemini (Google):** Machine learning dataset analysis, telemetry visualization scripts, and documentation review.

## Repository Structure

```text
NANORISCV-C2/
├── Design/
├── Schematics/
├── simulations/
├── timing_constraints/
└── README.md
