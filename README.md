# Synchronous FIFO in Verilog HDL

## 📌 Overview
This project implements a **parameterized synchronous FIFO (First-In-First-Out) buffer**
using **Verilog HDL**. The FIFO operates in a **single clock domain** and provides
controlled data buffering with **Full** and **Empty** status flags to prevent
overflow and underflow conditions.

The design is written in **synthesizable RTL style** and verified using simulation
in **Xilinx Vivado**.

---

##  Design Parameters
The FIFO is configurable using Verilog parameters:

- `data_width` : Width of each data word (default = 32 bits)
- `fifo_depth` : Number of FIFO entries (default = 8)

This makes the design reusable across different applications.

---

##  Module Interface

### Inputs
- `clk`   : System clock (single clock domain)
- `rst`   : Active-low asynchronous reset
- `cs`    : Chip select (enables FIFO operation)
- `wr_en` : Write enable signal
- `rd_en` : Read enable signal
- `data_in[data_width-1:0]` : Input data to be written into FIFO

### Outputs
- `data_out[data_width-1:0]` : Output data read from FIFO
- `empty` : Indicates FIFO is empty
- `full`  : Indicates FIFO is full

---

##  Internal Architecture

### Memory Array

-'reg [data_width-1:0] fifo [0:fifo_depth-1];'


- `localparam fifo_depth_log = $clog2(fifo_depth);`Pointer Logic 
- `reg [fifo_depth_log:0] `write_pointer;
- `reg [fifo_depth_log:0]` read_pointer; 

---
## Verification

**A dedicated testbench is used to verify:**

- Correct write and read operations  
- Proper assertion of full and empty flags  
- FIFO ordering behavior  
- Simulation performed using Vivado Simulator  
- Waveforms analyzed to validate functionality  
