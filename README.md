# RISC-V Single-Cycle Processor in Verilog

A 32-bit RISC-V (RV32I) single-cycle processor implemented in Verilog for the Digilent Basys 3 FPGA. 

## 🚀 Features

*   **Architecture:** 32-bit Single-Cycle Data Path and Control Unit
*   **Hardware Description Language:** Verilog
*   **Target FPGA:** Digilent Basys 3 (Artix-7)
*   **Supported Instructions:**
    *   **Arithmetic:** `add`, `sub`, `addi`
    *   **Logical:** `and`, `or`
    *   **Memory Access:** `lw` (Load Word), `sw` (Store Word)
    *   **Control Flow:** `beq` (Branch if Equal), `jal` (Jump and Link)

## ⚠️ Important Implementation Notes (Program Counter & Clock)

*   **Program Counter (PC) Initialization:** To prevent the simulation from getting stuck in an unknown state (`XXXXXXXX`), the `program_counter` module uses an inline `initial` block to force the PC to start at `32'b0`. This ensures the instruction memory fetches the first valid instruction on startup without requiring an external hardware reset signal.
*   **Clock Divider & Simulation:** The top-level FPGA connector (`basys3_connector.v`) includes a 25-bit counter to divide the 100MHz board clock into a slow clock for the CPU. **Do not simulate the `basys3_connector` module**, as it will require millions of simulated cycles to produce a single CPU clock tick. Always use `tb_main_module.v` as the Top Module for simulation to bypass the divider and feed a clock directly to the CPU.

## 🗂️ Project Structure

*   `main_module.v` - The top-level CPU wrapper connecting the datapath and control unit.
*   `PC.v`, `pc_adder.v`, `pc_target.v`, `pc_next_decider.v` - Program Counter logic, sequential updating, and branch target calculation.
*   `ALU_main.v`, `Alu_control_unit.v`, `ALU_mux.v` - Arithmetic Logic Unit, its instruction decoder, and source routing.
*   `main_control_unit.v` - Generates multiplexer and write-enable signals based on opcodes.
*   `register_file.v` - 32x32-bit integer register file.
*   `immediate_gen.v` - Handles sign-extension for various instruction formats (I, S, B, J).
*   `instr_mem.v` & `main_memory.v` - Instruction and Data memory modules.
*   `write_back.v` - Handles routing data back to the register file (supports standard operations and JAL).
*   `basys3_connector.v` - Top module for FPGA implementation, including the clock divider.
*   `basys3_constraints.xdc` - Xilinx physical constraint file mapping I/O to the Basys 3 board.
*   `tb_main_module.v` - Testbench for running behavioral simulations.

## 🛠️ Prerequisites

To simulate or synthesize this project, you will need:
*   [Xilinx Vivado](https://www.xilinx.com/products/design-tools/vivado.html) (WebPACK / ML Standard Edition is free)
*   (Optional) Digilent Basys 3 FPGA board for physical hardware testing

## 💻 Simulation / How to Run

1. Clone this repository:
   ```bash
   git clone [https://github.com/Nithish-Reddy360/riscv-single-cycle-core.git](https://github.com/Nithish-Reddy360/riscv-single-cycle-core.git)

   Open Vivado and create a new project.

1.Add all .v files to the Design Sources.

2.Add the basys3_constraints.xdc file to the Constraints.

3.Add tb_main_module.v to the Simulation Sources.

4.Crucial Step: Right-click tb_main_module.v in the Sources pane and select Set as Top.

5.Click Run Simulation -> Run Behavioral Simulation.

6.In the waveform window, expand the uut scope and drag the internal wires (like PC, Instr, SrcA, SrcB, and ALUResult) into the viewer to verify execution.

## 🔌 FPGA Implementation
In Vivado, set basys3_connector.v as the Top Module for synthesis.

Click Generate Bitstream.

Open the Hardware Manager, connect your Basys 3 board, and click Program Device.

The processor's lower 16 bits of ALU output are mapped directly to the 16 on-board LEDs.
