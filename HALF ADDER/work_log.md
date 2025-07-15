# HALF ADDER - Work Log
**Date:** July 9, 2025  
Started this part of the project...

# 🧮 HALF ADDER – Step-by-Step Simulation Guide

## 📅 Date: July 2025  
## 👤 Author: Maaz (Electrical Engineering Student)

---

## 🔧 TOOLS & SETUP

- **OS:** Ubuntu 20.04 or newer
- **Terminal:** Ubuntu default
- **Text Editor:** nano / gedit
- **Verilator:** For Verilog simulation
- **GTKWave:** For waveform viewing

---

## 📁 STEP 1: Create Project Folder & Verilog File

### 📌 Terminal Commands:
```bash
mkdir half_adder_project
cd half_adder_project
touch half_adder.v
nano half_adder.v
```

### 💡 Verilog Code:
```verilog
module half_adder(A, B, Carry, Sum);
  input A, B;
  output Carry, Sum;

  assign Carry = A & B;
  assign Sum = A ^ B;
endmodule
```

📸 ![Half Adder Code](images/code.png)

---

## 🧪 STEP 2: Install Verilator

### 📌 Terminal Commands:
```bash
sudo apt update
sudo apt install verilator
verilator --version
```

### ⚠️ Problems Faced:
- `Command 'verilator' not found` → Fixed using `sudo apt install verilator`
- **Old version** installed by default → (Optional fix using PPA or manual build)

📸 ![Verilator Terminal](images/verilator_installed.png)

---

## 👨‍💻 STEP 3: Create C++ Testbench

### 📌 Terminal Commands:
```bash
touch testbench.cpp
nano testbench.cpp
```

### 💡 Testbench Code:
```cpp
#include "Vhalf_adder.h"
#include "verilated.h"
#include "verilated_vcd_c.h"

int main(int argc, char** argv, char** env) {
    Verilated::commandArgs(argc, argv);
    Vhalf_adder* top = new Vhalf_adder;

    Verilated::traceEverOn(true);
    VerilatedVcdC* tfp = new VerilatedVcdC;
    top->trace(tfp, 99);
    tfp->open("wave.vcd");

    for (int A = 0; A <= 1; A++) {
        for (int B = 0; B <= 1; B++) {
            top->A = A;
            top->B = B;
            top->eval();
            tfp->dump(10 * (2 * A + B));
            printf("A=%d B=%d | Sum=%d Carry=%d\n", A, B, top->Sum, top->Carry);
        }
    }

    tfp->close();
    delete top;
    delete tfp;
    return 0;
}
```

📸 ![Testbench](images/testbench.png)

---

## ⚙️ STEP 4: Compile & Simulate the Design

### 📌 Terminal Commands:
```bash
verilator -Wall --cc half_adder.v --exe testbench.cpp --trace
make -C obj_dir -j -f Vhalf_adder.mk Vhalf_adder
./obj_dir/Vhalf_adder
```

### ⚠️ Problems Faced:
- `make: command not found` → Fixed using:
```bash
sudo apt install build-essential
```
- Typo: `top>Sum` → corrected to `top->Sum`
- Missed `endmodule` in Verilog

📸 ![Compile Terminal](images/compile_error_fixed.png)

---

## 📊 STEP 5: View Waveform in GTKWave

### 📌 Terminal Commands:
```bash
sudo apt install gtkwave
gtkwave wave.vcd
```

- GTKWave GUI opens
- Check transitions for A, B, Sum, and Carry

📸 ![GTKWave](images/waveform.png)

---

## ❗ COMMON MISTAKES I MADE

| ❌ Mistake | ✅ Fix |
|-----------|--------|
| Forgot `endmodule` | Added it to end of Verilog file |
| Typo `top>Sum` | Corrected to `top->Sum` |
| Verilator not installed | Installed using apt |
| `make` command missing | Installed with `build-essential` |

---

## 💡 BEGINNER TIPS (Ubuntu/Terminal)

- Use `ls` to list files, `cd` to enter folders
- Use `nano filename` to edit a file
- Use `Ctrl + O` to save in nano, `Ctrl + X` to exit
- Always update packages first: `sudo apt update`
- Use `gedit` if you prefer a graphical editor

---

## ✅ CONCLUSION

- ✅ Half Adder simulation completed using Verilator
- ✅ GTKWave used to confirm waveform behavior
- 🛠️ Faced real beginner problems and solved them
- 🧠 Improved confidence using terminal, Verilog, and waveform analysis

---

📁 *All images used are in the `/images` folder inside the HALF ADDER directory.*

