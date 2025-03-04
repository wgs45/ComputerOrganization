# 🌟 MIPS Instructions

---

## 🎯 MIPS R-Format Instructions

### 📝 Instruction Format

| 🔢 op (6 bits) | 🔢 rs (5 bits) | 🔢 rt (5 bits) | 🔢 rd (5 bits) | 🔢 shamt (5 bits) | 🔢 funct (6 bits) |
| -------------- | -------------- | -------------- | -------------- | ----------------- | ----------------- |

### 📌 Fields Description

- **🟢 op**: Operation code (opcode)
- **🔵 rs**: First source register operand
- **🟣 rt**: Second source register operand
- **🟠 rd**: Destination register operand
- **🟡 shamt**: Shift amount
- **🔴 funct**: Function code (extends opcode)

---

## 🔥 MIPS I-Format Instructions

### 📝 Instruction Format

| 🔢 op (6 bits) | 🔢 rs (5 bits) | 🔢 rt (5 bits) | 🏠 Constant/Address (16 bits) |
| -------------- | -------------- | -------------- | ----------------------------- |

### 📌 Fields Description

- **🟢 op**: Operation code (opcode)
- **🔵 rs**: Source register operand
- **🟣 rt**:
  - Destination register for **load word (lw)**
  - Source register for **store word (sw)**
- **🔢 Constant**: Immediate value (_-2^15 to +2^15 - 1_)
- **🏠 Address**: Offset added to base address in `rs`

---

## 💡 Design Principle: Good Design Demands Good Compromises

- ✨ Different formats complicate decoding but maintain uniform **32-bit instruction length**.
- ✨ Keeping formats as **similar as possible** simplifies understanding and implementation.

---

## 🏆 Examples

🔹 **R-Format Example:**

```assembly
add $t0, $t1, $t2   # $t0 = $t1 + $t2
```

🔹 **I-Format Example:**

```assembly
lw $t0, 0($t1)   # Load word from memory address in $t1 into $t0
sw $t0, 4($t1)   # Store word from $t0 into memory address in $t1 + 4
```
