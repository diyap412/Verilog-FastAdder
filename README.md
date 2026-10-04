# Verilog-FastAdder

# Verilog FastAdder

**Verilog FastAdder** is a high-speed, configurable-width adder implemented in SystemVerilog. The design uses a pipelined architecture to improve timing performance while supporting multiple adder widths.

## Overview

FastAdder is a parameterized arithmetic core that performs binary addition with **carry-in** and **carry-out** support. The adder width can be customized using a single `width` parameter, allowing the same design to be used for different bit-width requirements.

The design was optimized primarily for **timing performance** and evaluated using **Xilinx Vivado** through synthesis and static timing analysis.

## Core Interface

The top-level module is `adder`, located in `adder.sv`.

| **Port** | **Direction** | **Width** | **Description** |
| -------- | ------------- | --------: | --------------- |
| `clk_i`  | Input         |         1 | Clock input     |
| `cin_i`  | Input         |         1 | Carry-in        |
| `a_i`    | Input         |   `width` | First operand   |
| `b_i`    | Input         |   `width` | Second operand  |
| `out_o`  | Output        |   `width` | Addition result |
| `cout_o` | Output        |         1 | Carry-out       |

## Configurable Width

The `width` parameter determines the number of bits used by the adder.

For example, setting `width` to `16` creates a **16-bit adder**.

## Instantiation

### SystemVerilog

```systemverilog
adder #(
    .width(16)
) adder_inst (
    .clk_i(clk),
    .cin_i(cin),
    .a_i(a),
    .b_i(b),
    .out_o(out),
    .cout_o(cout)
);
```

### VHDL

```vhdl
adder_inst : adder
generic map (
    width => 16
)
port map (
    clk_i => clk,
    cin_i => cin,
    a_i => a,
    b_i => b,
    out_o => out,
    cout_o => cout
);
```

## Performance Evaluation

Performance was the primary design objective, so FastAdder uses a **pipelined architecture** to improve maximum operating frequency.

Performance was evaluated using **Xilinx Vivado 2019.2** through synthesis and static timing analysis. The target device was the **Xilinx Zynq XC7Z020CLG400-1 FPGA**.

FastAdder was compared against the **Xilinx Adder/Subtractor IP core** using functionally equivalent configurations and identical pipeline latency.

## Maximum Frequency

FastAdder achieved up to a **50% improvement in maximum operating frequency** compared with the equivalent Xilinx Adder configuration.

| **Width** | **FastAdder** | **Xilinx Adder** |
| --------- | ------------: | ---------------: |
| 16-bit    |       450 MHz |          390 MHz |
| 32-bit    |       450 MHz |          300 MHz |
| 64-bit    |       450 MHz |          300 MHz |

## Resource Utilization

The increased performance comes with a moderate increase in FPGA resource usage.

| **Width** | **FastAdder**               | **Xilinx Adder** |
| --------- | --------------------------- | ---------------- |
| 16-bit    | 16 LUT, 42 FF               | 16 LUT, 33 FF    |
| 32-bit    | 40 LUT, 8 LUTRAM, 164 FF    | 33 LUT, 99 FF    |
| 64-bit    | 168 LUT, 104 LUTRAM, 350 FF | 123 LUT, 247 FF  |

The additional resource usage represents a tradeoff for the higher operating frequency achieved through the pipelined architecture.

## Future Improvements

* Add **subtraction support**
* Support **more than two input operands**
* Explore additional **adder architectures**
* Optimize different **pipeline configurations**
* Evaluate performance across additional **FPGA families**
* Expand verification with additional **simulation and testbench coverage**

## Technologies

* **SystemVerilog**
* **FPGA Design**
* **Digital Logic**
* **Pipelined Architecture**
* **RTL Design**
* **Xilinx Vivado**
* **Static Timing Analysis**
* **Hardware Verification**
