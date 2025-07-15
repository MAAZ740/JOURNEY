# HALF ADDER - Work Log
**Date:** July 9, 2025  
Started this part of the project...

# HALF ADDER – Verilog Implementation Report

## 🗓️ Date Started: July 15, 2025

---

## ✅ Step-by-Step Progress

### 1. ✍️ Wrote Verilog Code
- Module for half adder created using `assign` statements.
- Code saved as `half_adder.v`
- ![Verilog Code](images/code.png)

### 2. ⚙️ Compiled the Code
- Used `iverilog` in Ubuntu terminal
- Compilation successful ✅
- ![Compilation Terminal](images/terminal.png)

### 3. 🔬 Simulated with GTKWave
- Dumped VCD file using testbench
- Opened waveform in GTKWave
- Signals displayed correctly
- ![GTKWave Output](images/wave.png)

---

## 🛠️ Problems & Fixes

| Problem | Solution |
|--------|----------|
| Forgot to dump VCD file | Added `$dumpfile` and `$dumpvars` in testbench |
| GTKWave not launching | Installed GTKWave using `sudo apt install gtkwave` |
| Incorrect waveform | Fixed clock signal in testbench |

---

## 📌 Summary
- Half Adder code works ✅
- Simulation successful
- Learned to debug GTKWave and Verilog testbenches
