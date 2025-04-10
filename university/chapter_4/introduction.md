# 🧠 **CPU Architecture & Instruction Execution** ⚙️

---

## 🚀 **Introduction to CPU Performance**

🔍 Key Factors That Impact CPU Performance:

1. **Instruction Count**

   - 📌 Determined by **ISA (Instruction Set Architecture)** and the **compiler**

2. **CPI (Cycles Per Instruction)** & **Cycle Time**
   - 🔧 Determined by the **CPU hardware**

🛠️ We will analyze two MIPS implementations:

- ✅ A simplified version: **One clock cycle per instruction**
- ⏩ A realistic **pipelined version** (covered in §4.5 and later)

📦 The instruction set includes:

- **Memory-reference:** `lw`, `sw`
- **Arithmetic/Logic:** `add`, `sub`, `and`, `or`, `slt`
- **Control Transfer:** `beq`, `j`

---

## 📋 **Instruction Execution Steps**

🔁 For every instruction, the **first two steps** are **always the same**:

1. 🧭 **Fetch** the instruction from memory:

   - `PC` → **Instruction Memory**

2. 📥 **Read registers** from the register file:
   - Extract **register numbers**

🔧 Then, depending on the **instruction class** (except `j`), do the following:

- 🧮 Use the **ALU** to calculate:

  - Arithmetic result → `add`, `sub`, `and`, `or`, `slt`
  - Memory address → `lw`, `sw`
  - Branch target → `beq`

- 💾 Access **data memory** for `lw` and `sw`

- 🧭 Update the **Program Counter (PC)**:
  - For branches: `PC ← target address`
  - For others: `PC ← PC + 4`

---

## 🧠 **CPU Design Overview**

The CPU can be broken into several fundamental components, each playing a key role in instruction execution:

### 🧰 **Core Components**

- **Program Counter (PC):** Holds the address of the current instruction.
- **Instruction Memory:** Stores all instructions for the program.
- **Register File:** Contains a small, fast memory bank for temporary values and variables.
- **ALU (Arithmetic Logic Unit):** Performs calculations and logic operations.
- **Data Memory:** Stores and retrieves data from RAM.

### 🔀 **Data Control and Routing**

- **Multiplexers (MUXes):**

  - Direct signals to different components based on control signals.
  - Help select between values like immediate vs. register data, or ALU result vs. memory output.

- **Control Unit:**
  - Decodes instructions.
  - Generates control signals that guide the movement of data.
  - Manages how and when the ALU, memory, and registers interact.

### 🛣️ **Instruction Path (Simplified)**

```text
  [PC] → [Instruction Memory] → [Decoder] → [Register File] ↘
                                                     ↘→ [ALU] → [Data Memory]
                                                             ↘→ [Write Back to Registers]
```

Each instruction type (e.g., `lw`, `add`, `beq`) follows a slightly different path through the CPU, controlled by signals from the Control Unit.

---

💡 **Study Tip:** Try drawing the data path for each instruction type! It helps visualize how the control signals and hardware components interact during execution. 🖊️🧩
