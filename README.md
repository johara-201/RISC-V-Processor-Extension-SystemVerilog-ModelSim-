# RISC-V Processor Extension – SystemVerilog, ModelSim

## Project Overview
This project was part of a Digital Systems course.  
We were provided with a working multi-cycle RISC-V processor implementation in SystemVerilog.  
Our task was to extend the processor by adding support for a custom instruction and to verify it using simulation.

## Custom Instruction
- Added a new instruction:  
  ```
  R[rd] = (R[rs1] + imm) ^ 0xFFFFFFFF
  ```
- Required changes:
  - Update datapath to support an additional ALU path.
  - Extend the control FSM with new states for the instruction.
  - Update RTL modules (`rv_ctl.sv`, `rv_dp.sv`, `params.inc`).

## Verification
- Wrote a test program in RISC-V assembly (`test.s`) that executes the new instruction.
- Generated `imem.hex` and `dmem_init.hex` for simulation.
- Used ModelSim to run the design and analyzed waveforms (`clk`, `pc`, `ir`, ALU signals, memory interface).
- Verified correctness by checking:
  - Expected memory writes in `dmem_out.hex`
  - Correct behavior in waveform analysis

## Files in this Repository
- `rv_top.sv` – Top hierarchy of the processor  
- `rv_dp.sv` – Datapath module  
- `rv_ctl.sv` – Control FSM  
- `rv_sim.sv` – Simulation wrapper  
- `params.inc` – Instruction and ALU parameter definitions  
- `test.s` – Assembly test program  
- `imem.hex`, `dmem_init.hex` – Memory initialization files  

## How to Run (ModelSim)
```sh
rm -rf work; vlib work
vlog *.sv
vsim -c rv_sim -do "run -all; quit"
```

