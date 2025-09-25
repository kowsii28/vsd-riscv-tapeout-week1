# 📘 Day 4 — Gate Level Simulation (GLS) & Synthesis-Simulation Mismatch  

## 🎯 Objectives
- Understand **Gate Level Simulation (GLS)** and its purpose.  
- Learn the differences between **Timing-Aware and Functional Gate Level Models**.  
- Explore common **synthesis-simulation mismatches** and their causes.  
- Learn proper **Verilog coding practices** to avoid mismatch.  
- Perform **GLS using Yosys and Iverilog**, generate waveforms, and analyze outputs.  

---

## 📖 Theory / Background  

### 🔹 a. Gate Level Simulation (GLS)
- GLS is a simulation at the **gate level using the synthesized netlist**.  
- Purpose: verify that **synthesized netlist behaves identically** to RTL code under the same testbench.  
- Netlist is logically equivalent to RTL but mapped to **standard cells**.  
- Same testbench can be used for both **RTL** and **Gate Level Netlist**.  

---

### 🔹 b. Types of Gate Level Verilog Models
1. **Functional Model**: models the logic functionality only, without timing.  
2. **Timing-Aware Model**: includes **delays and timing information** along with functionality.  
   - Timing-Aware = Functional + Timing delays  

---

### 🔹 c. Synthesis-Simulation Mismatch
Common issues when GLS output differs from RTL simulation:

1. **Missing Sensitivity List**
   - Always blocks with incomplete sensitivity lists can lead to **incorrect simulation**.  
   - Recommended: use `always @(*)` for combinational logic.  
   - Avoid specifying individual signals manually in the sensitivity list.  

2. **Blocking vs Non-Blocking Assignments**
   - Incorrect use can cause **different outputs in RTL vs GLS**.  
   - **Blocking (`=`)** executes sequentially; may cause issues in combinational logic.  
   - **Non-blocking (`<=`)** executes in parallel at clock edge; suitable for sequential logic.  

3. **Non-Standard Verilog Coding**
   - Using non-standard or poorly written code can result in mismatches after synthesis.  
   - Surprisingly, **synthesis tools may correct some RTL coding issues**, leading to successful gate-level behavior.  

---

### 🔹 d. Workflow for GLS
1. **Synthesize RTL using Yosys** to generate a gate-level netlist.  
2. **Use Iverilog** to run simulations:  
   - Provide **standard cell library** (from your GitHub repo).  
   - Provide **netlist file** and **testbench file**.  
3. **Run simulation**:  

iverlog 2 verilog files for std cells netlist testbench
./a.out                  # Execute simulation
gtkwave filename.vcd

### 🔹 e. GTKWave Analysis & Synthesis-Simulation Verification

- **Generate GTKWave output** to analyze signals visually.  
- Verified **synthesis-simulation mismatches** for blocking vs non-blocking assignments by:
  1. Simulating RTL normally → observe outputs.  
  2. Synthesizing RTL → running gate-level simulation → observe mismatches.  
  3. Analyzing waveforms in GTKWave for timing and logic differences.  

---

## 🔬 Lab / Practical Work

- Synthesized designs using **Yosys** for Gate Level Simulation (GLS).  
- Worked with **netlist files, testbench files, and standard cell Verilog files**.  
- Ran simulations using **Iverilog**, generating `.vcd` files for GTKWave visualization.  
- Observed differences between **RTL simulation** and **GLS outputs**.  
- Identified issues caused by:
  - **Missing sensitivity lists** (`always @(*)` recommended).  
  - **Blocking vs non-blocking assignment mismatches**.  
  - **Non-standard Verilog constructs**.  
- Verified **timing-aware vs functional gate-level models** for accuracy and timing behavior.  

---

## 📊 Observations

- GLS confirms that the **synthesized netlist matches RTL logic** under the same testbench.  
- **Missing sensitivity lists** can cause incorrect or inconsistent outputs.  
- **Blocking vs non-blocking assignments** are a common source of mismatch.  
- Synthesis tools may automatically **correct some RTL issues**.  
- **Timing-aware models** provide accurate signal timing; **functional models** focus on logic correctness.  

---

## ✅ Conclusion / Key Takeaways

- **GLS is essential** to verify gate-level behavior against RTL.  
- Proper **Verilog coding practices** (sensitivity lists, assignment types) prevent mismatches.  
- **Timing-aware simulations** provide better verification for real-world delays.  
- Synthesis tools can **resolve some coding issues**, but clean RTL remains critical.  
- Visualization tools like **GTKWave** help analyze and debug mismatches efficiently.  
