# 🏗️ **Building a Datapath** 💡

---

## 🧠 **What is a Datapath?**

A **datapath** consists of the elements in a CPU that **process data and addresses**. These elements include:

- **Registers**
- **ALUs (Arithmetic Logic Units)**
- **Multiplexers (mux)**
- **Memory units**

We'll build a **MIPS datapath** step-by-step, starting with a **basic overview design**.

---

## ⚙️ **Datapath Elements**

### 1. 🧠 **Instruction Memory**

- **Purpose**: Stores the program's instructions.
- **Function**: Supplies instructions based on an address provided by the **Program Counter (PC)**.

---

### 2. 🖥️ **Program Counter (PC)**

- **Purpose**: A special register that holds the **address** of the current instruction.
- **Function**: Increments by **4** after each instruction to point to the next instruction in memory.

---

### 3. ➕ **Adder**

- **Purpose**: **Increments the PC**.
- **Function**: Calculates the address of the next instruction by adding 4 to the current PC.

---

## 📝 **Types of Instructions**

### 🔧 **R-type Instructions (Register-type)**

- **Steps**:

  1. **Read** two operands from the register file.
  2. **Perform arithmetic/logic operations** (e.g., `add`, `sub`, `and`).
  3. **Write the result** back to a register in the register file.

- **Components**:
  - **Register File** (5 bits for the register number, 1 bit for the branch signal, and 32 bits for the data).

---

### 📦 **Load/Store Instructions**

- **Steps**:
  1. **Read** register operands (for `load` and `store` instructions).
  2. **Calculate the address** using a 16-bit offset:
     - **Use ALU** to add the offset and base address (sign-extend offset to 32 bits).
  3. **Memory access**:
     - **Load**: **Read from memory** and update the register.
     - **Store**: **Write data from register** to memory.

---

### 🚪 **Branch Instructions**

- **Steps**:
  1. **Read register operands**.
  2. **Compare operands**:
     - **Use ALU** to subtract and check the **Zero output** (for equality).
  3. **Calculate target address**:
     - **Sign-extend** the displacement.
     - **Shift left 2 bits** to match word displacement.
     - **Add to PC + 4** (already calculated during instruction fetch).
  4. **Determine branch condition**:
     - **If true**: Branch is taken → Set **PC** to **target address**.
     - **If false**: No branch → Set **PC** to **PC + 4** (next instruction).

---

## 🔄 **Creating a Single Datapath**

The **simplest datapath** tries to execute all instructions in a **single clock cycle**.

### ⚡ Key Principles:

- **No datapath resource** can be used more than once per instruction.
  - **Replication required** for elements used multiple times.
  - Example: Separate **instruction memory** and **data memory**.
- **Sharing elements** where possible.
  - **Multiplexers (mux)** are used to select alternate data sources for different instructions.

---

## 💥 **Diagram**: R-type/Load/Store Datapath

Below is an illustration of the **R-type / Load/Store datapath** design.

### 🌟 **Full Datapath**

```
[PC]  → [Instruction Memory] → [Control Unit] → [ALU] → [Register File] → [Data Memory]
         ↑                        ↑       ↑
         |                        |       |
    [Adder (PC+4)]      [ALU Source]     |
         |                 ↑             |
         |                 |             ↓
    [Mux] <--> [Mux] --> [Mux] --> [Result (Write back)]
```

### 🧩 **Key Connections**:

- **PC**: Tracks instruction sequence.
- **Instruction Memory**: Stores the instructions.
- **Control Unit**: Directs the flow based on opcode.
- **ALU**: Performs calculations and comparisons.
- **Register File**: Holds operand registers and results.
- **Data Memory**: Stores data for load/store operations.
- **Muxes**: Select between multiple inputs based on the instruction type.
