# RISC-V Single-Cycle Processor in Verilog

A complete, fully functional 32-bit RISC-V single-cycle processor implemented in Verilog. This core is based on the RV32I base integer instruction set and is designed for synthesis and implementation on the Digilent Basys 3 FPGA board.

## 🚀 Features

*   **Architecture:** 32-bit Single-Cycle Data Path and Control Unit
*   **Hardware Description Language:** Verilog
*   **Target FPGA:** Basys 3 (Artix-7)
*   **Supported Instructions:**
    *   **Arithmetic:** `add`, `sub`, `addi`
    *   **Logical:** `and`, `or`
    *   **Memory Access:** `lw` (Load Word), `sw` (Store Word)
    *   **Control Flow:** `beq` (Branch if Equal), `jal` (Jump and Link)

## 🗂️ Project Structure

*   `main_module.v` - The top-level CPU wrapper connecting the datapath and control unit.
*   `ALU_main.v` & `Alu_control_unit.v` - Arithmetic Logic Unit and its instruction decoder.
*   `main_control_unit.v` - Generates multiplexer and write-enable signals based on opcodes.
*   `register_file.v` - 32x32-bit integer register file.
*   `instr_mem.v` & `main_memory.v` - Instruction and Data memory modules.
*   `basys3_connector.v` - Top module for FPGA implementation, including a clock divider.
*   `basys3_constraints.xdc` - Xilinx physical constraint file mapping I/O to the Basys 3 board.
*   `tb_main_module.v` - Testbench for running behavioral simulations.

## 🛠️ Prerequisites

To simulate or synthesize this project, you will need:
*   [Xilinx Vivado](https://www.xilinx.com/products/design-tools/vivado.html) (WebPACK / ML Standard Edition is free)
*   (Optional) Digilent Basys 3 FPGA board for physical hardware testing

## 💻 Simulation / How to Run

1. Clone this repository:
   ```bash
   git clone [https://github.com/YourUsername/Your-Repo-Name.git](https://github.com/YourUsername/Your-Repo-Name.git)
