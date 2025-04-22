# 🎯 ALU Control – Guide 💻✨

---

### 🔧 **What is ALU Used For?**

- **Load/Store** → `F = ADD` ➕
- **Branch** → `F = SUBTRACT` ➖
- **R-Type Instructions** → `F = Depends on funct field` 🧠

---

### 🔑 **ALU Control Function Table**

| ALU Control | Function               | Opcode Use 💡         |
| ----------- | ---------------------- | --------------------- |
| `0000`      | AND                    | R-type 🧠             |
| `0001`      | OR                     | R-type 🧠             |
| `0010`      | ADD                    | Load/Store, R-type ➕ |
| `0110`      | SUBTRACT               | Branch, R-type ➖     |
| `0111`      | Set-On-Less-Than (SLT) | R-type ⬇️             |
| `1100`      | NOR                    | R-type ❌             |

---

### 🧩 How is ALU Control Generated?

1. **Main Control Unit** 🧠 ➝ Generates **2-bit `ALUOp`** from the instruction **opcode** 🧾
2. **ALU Control Logic** 💡 ➝ Uses `ALUOp` + `funct` (for R-type) to create 4-bit ALU control signal 🎯

This **modular design** keeps the main control unit simpler and more efficient ✅

---

### 🔍 Instruction Breakdown + ALU Control 🔽

| Instruction  | ALUOp | Operation    | `funct`  | ALU Function | ALU Control |
| ------------ | ----- | ------------ | -------- | ------------ | ----------- |
| `lw` (0x23)  | `00`  | Load Word    | `X`      | ADD          | `0010` ➕   |
| `sw` (0x2B)  | `00`  | Store Word   | `X`      | ADD          | `0010` ➕   |
| `beq` (0x04) | `01`  | Branch Equal | `X`      | SUBTRACT     | `0110` ➖   |
| `R-type`     | `10`  | ADD          | `100000` | ADD          | `0010` ➕   |
|              |       | SUBTRACT     | `100010` | SUBTRACT     | `0110` ➖   |
|              |       | AND          | `100100` | AND          | `0000` 🔗   |
|              |       | OR           | `100101` | OR           | `0001` 🔗   |
|              |       | SLT          | `101010` | Set < Than   | `0111` ⬇️   |

> ✨ **Note:** `X = don’t care` when funct is irrelevant 😌

---

### 🧬 Instruction Fields Breakdown

#### 🧠 R-Type Format

`opcode (6)` | `rs` | `rt` | `rd` | `shamt` | `funct`  
`31:26` → `0` | | | | | ALU action determined by `funct` 🧠

#### 📦 Load/Store

`opcode (6)` | `rs` | `rt` | `immediate`  
Accessing memory using base register 🧠

#### 🚪 Branch

`opcode (6)` | `rs` | `rt` | `offset`  
Conditional jump using subtraction ➖

---

### 🚀 Implementing Jumps

- **Jump Instruction (opcode = 2)**  
  ➝ **PC =** `{upper 4 bits of PC, 26-bit jump address, 00}`  
  ➝ Unconditional jump 🏃‍♂️💨  
  ➝ Needs a **special control signal** decoded from `opcode`

---

## ⏱️ Pipelining Performance Notes

- **⌛ Longest delay = clock period**
- **Critical path**: `Load` instruction  
  🧱 IM → RF → ALU → DM → RF
- CPI = 1 ✅ BUT 🕓 Clock cycle too long!

> 🔧 Design Principle: Optimize the **worst-case path** to improve the whole system — **not just the average** 💡
