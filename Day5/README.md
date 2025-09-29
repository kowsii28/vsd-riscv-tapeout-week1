# 📘 Day 5 — Case Statements, Loops, and Latch Inference  

## 🎯 Objectives
- Understand the difference between **IF-ELSE** and **CASE** statements.  
- Learn about **inferred latches** and how incomplete case statements can cause issues.  
- Explore **FOR loops** and **GENERATE FOR loops** in Verilog.  
- Apply loops for efficient instantiation of hardware modules like **MUX**, **DEMUX**, and **adders**.  

---

## 📖 Theory / Background  

### 🔹 IF-ELSE vs CASE  
- **IF-ELSE**: priority-based (top-to-bottom). Once a condition is true, others are skipped.  
- **CASE**: checks multiple conditions in parallel.  
- ⚠️ **Caveat**: Incomplete `CASE` statements (not covering all conditions) lead to **inferred latches**, which can cause unintended storage elements and incorrect design behavior.  
- Always ensure:  
  - Use **`always @(*)`** for combinational logic.  
  - Cover all input/output conditions in a `CASE` block.  

---

### 🔹 Inferred Latches  
- Caused by **partial assignment** or **incomplete CASE/IF statements**.  
- If not all conditions are defined, the synthesizer infers a latch to hold previous values.  
- In FSMs or counters, this can result in **unexpected glitches or incorrect outputs**.  

---

### 🔹 FOR vs GENERATE FOR Loops  
- **FOR loop (inside always block):**  
  - Used in procedural code for repetitive logic within `always`.  
  - Example: iterating over inputs of a **MUX/DEMUX**.  

- **GENERATE FOR loop (outside always block):**  
  - Used to **instantiate multiple hardware blocks** (structural replication).  
  - Great for parameterized designs like **N-bit adders**, **DEMUX**, or replicated logic.  

✅ Benefit: Using loops reduces code size, improves readability, and makes designs scalable.  

---

## 🔬 Lab / Practical Work  

1. **Case Statement Exploration**  
   - Wrote `CASE` statement examples for counters.  
   - Tested **incomplete vs complete CASE statements**.  
   - Verified that incomplete CASE → **inferred latch** → incorrect design.  

2. **FOR Loops**  
   - Implemented **MUX/DEMUX designs** using procedural FOR loops.  
   - Observed how loop iteration scales the number of inputs/outputs.  

3. **GENERATE FOR Loops**  
   - Implemented **DEMUX using GENERATE** for modular hardware instantiation.  
   - Designed **multi-bit full adders** using replicated logic.  
   - Verified output correctness for different loop iterations.  

---

## 📊 Observations  
- **IF-ELSE** is priority-based; **CASE** allows parallel condition checking.  
- Incomplete CASE statements caused **latch inference**, leading to unstable outputs.  
- **FOR loops** simplified coding for large multiplexers/demultiplexers.  
- **GENERATE FOR loops** enabled scalable hardware design (e.g., N-bit adders).  
- Using loops made designs more **efficient, modular, and parameterized**.  

---

## ✅ Conclusion / Key Takeaways  
- Always cover all possible conditions in a `CASE` block to **avoid latch inference**.  
- Use `always @(*)` for combinational logic to prevent mismatches.  
- **FOR loops** → good for behavioral logic.  
- **GENERATE FOR loops** → best for hardware instantiation.  
- Loops and CASE constructs improve **efficiency, scalability, and readability** of RTL design.  
