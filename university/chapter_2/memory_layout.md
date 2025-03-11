# 🧠 Memory in MIPS

---

## 🏗️ Memory Layout

| 📌 Reserved      | 📜 Text     | 📦 Static Data    | 📊 Dynamic Data / Stack |
| ---------------- | ----------- | ----------------- | ----------------------- |
| PC → `0040 0000` | `1000 0000` | $gp → `1000 8000` | $sp → `7fff fffc`       |

🔹 **Left to right** represents **bottom to top** in memory. 📈

### 📂 Segments Explained

1️⃣ **Text Segment** 📜: Stores MIPS machine code (instructions)
2️⃣ **Static Data** 📦: Stores global/static variables, constants, strings

- `$gp` (Global Pointer) initialized for efficient access
  3️⃣ **Dynamic Data (Heap)** 🏗️: Used for dynamic memory allocation (e.g., `malloc` in C, `new` in Java)
  4️⃣ **Stack** 📊: Stores automatic/local variables, grows downward

---

## 🔢 32-bit Constants in MIPS

- Most constants fit in **16-bit immediates** ✅
- For **32-bit constants**, use:

```assembly
lui rt, constant  # Load Upper Immediate
```

📌 **How it works:**

- Copies **16-bit constant** into **upper 16 bits** of `rt` 🏗️
- **Clears lower 16 bits** to `0`

---

## 🔀 Branch Addressing in MIPS

### 🏗️ Branch Instructions (e.g., `beq`, `bne`)

| 🏷️ Opcode | 🎯 rs  | 🎯 rt  | 📌 Target Address |
| --------- | ------ | ------ | ----------------- |
| 6 bits    | 5 bits | 5 bits | 16 bits           |

### 📌 PC-Relative Addressing

- Target **address** = `PC + (offset × 4)`
- PC **auto-increments** by 4 before executing instruction
- Used for **forward & backward branches** 🔄

---

## 🚀 Jump Addressing in MIPS

### 📌 J-Type Instruction Format

| 🔢 Opcode | 🎯 Address |
| --------- | ---------- |
| 6 bits    | 26 bits    |

### 🎯 How Jumps Work

- **Jump (`j`) & Jump and Link (`jal`)** can target **anywhere** in text segment 📜
- Encodes **full address** inside the instruction
- Uses **(Pseudo) Direct Jump Addressing** 📍
- **Target Address** = `PC[31...28] : (address × 4)`
