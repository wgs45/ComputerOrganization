# 🌟 **MIPS Syntax Guide**

MIPS (Microprocessor without Interlocked Pipeline Stages) is a **RISC architecture** designed for efficient, low-level instruction execution. 🚀

---

## 🔲 **Logical Operations**

Logical operations enable **bitwise manipulations**, which are crucial for low-level programming.

| **Operation**   | **C** | **Java** | **MIPS**      |
| --------------- | ----- | -------- | ------------- |
| **Shift Left**  | `<<`  | `<<`     | `sll`         |
| **Shift Right** | `>>`  | `>>`     | `srl`         |
| **Bitwise AND** | `&`   | `&`      | `and`, `andi` |
| **Bitwise OR**  |       |          | `or`, `ori`   |
| **Bitwise NOT** | `~`   | `~`      | `nor`         |

### ✨ Key Points

- **Shift operations** manipulate bit positions efficiently.
- **AND operations** mask bits by selecting specific ones.
- **OR operations** toggle bits, and `NOR` inverts them.

---

## 🔁 **Shift Operations**

Shift operations move bits left or right, filling vacated positions with **zeros**. Useful for **multiplication and division** by powers of 2. 🔢

| 🔢 **op** (6 bits) | 🔢 **rs** (5 bits) | 🔢 **rt** (5 bits) | 🔢 **rd** (5 bits) | 🔢 **shamt** (5 bits) | 🔢 **funct** (6 bits) |
| ------------------ | ------------------ | ------------------ | ------------------ | --------------------- | --------------------- |

### 🔹 **Shift Left Logical (`sll`)**

- Moves bits **left**, filling with **0s**.
- Effect: Multiply by **2^i**.
- **Example:** `sll $t0, $t1, 2` → `$t1 * 4 → $t0`

### 🔹 **Shift Right Logical (`srl`)**

- Moves bits **right**, filling with **0s**.
- Effect: Divide by **2^i** (**unsigned numbers**).
- **Example:** `srl $t0, $t1, 2` → `$t1 / 4 → $t0`

Example:

```assembly
sll $t0, $t1, 2  # Shift left logical: $t0 = $t1 * 4 (2^2)
srl $t0, $t1, 2  # Shift right logical: $t0 = $t1 / 4 (2^2)
```

---

## 🛠️ **AND Operations**

Great for **masking** bits. 🧰

```assembly
and $t0, $t1, $t2  # Performs bitwise AND: $t0 = $t1 & $t2
```

- **AND** selects specific bits, clearing others.
- Useful for bit filtering and condition checks.

---

## 🔄 **OR Operations**

**OR** flips **0s to 1s**. Think of it like a **toggle switch**! 🔄

```assembly
or $t0, $t1, $t2  # Bitwise OR: $t0 = $t1 | $t2
nor $t0, $t1, $zero  # Bitwise NOT: $t0 = ~($t1)
```

- **`NOR`** = **NOT (A OR B)**
- Used for bitwise negation (`NOT` operation in MIPS).

---

## ⚖️ **Conditional Operations**

Enable **decision-making** by branching to instructions based on conditions. 💡

1. **Branch if Equal (`beq`)**

   ```assembly
   beq $t0, $t1, L1  # if ($t0 == $t1) jump to L1
   ```

2. **Branch if Not Equal (`bne`)**

   ```assembly
   bne $t0, $t1, L1  # if ($t0 != $t1) jump to L1
   ```

3. **Unconditional Jump (`j`)**

   ```assembly
   j L1  # Jump to L1
   ```

---

## 🏃 **Jumping to Labels**

Jumps allow flexible code execution. 🏃‍♂️💨

Example: **Compiling an `if-else` statement**

```c
if (i == j) f = g + h;
else f = g - h;
```

MIPS equivalent:

```assembly
bne $s3, $s4, Else
add $s0, $s1, $s2
j Exit

Else:
sub $s0, $s1, $s2

Exit:
```

---

## 🔁 **Loop Statements in MIPS**

Example: **Compiling a `while` loop**

```c
while (save[i] == k) i += 1;
```

**MIPS equivalent:**

```assembly
Loop:
sll $t1, $s3, 2        # Multiply i by 4 (word size)
add $t1, $t1, $s6      # Get address of save[i]
lw $t0, 0($t1)         # Load save[i] into $t0
bne $t0, $s5, Exit     # If save[i] != k, exit loop
addi $s3, $s3, 1       # i += 1
j Loop                 # Repeat the loop

Exit:
```

---

## ⚡ **More Conditional Operations**

- **Set result to `1` if condition is true, otherwise `0`.**

```assembly
slt rd, rs, rt  # if (rs < rt) rd = 1 else rd = 0
```

```assembly
slti rt, rs, constant  # if (rs < constant) rt = 1 else rt = 0
```

Example with branching:

```assembly
slt $t0, $s1, $s2 # if ($s1 < $s2)
bne $t0, $zero, L # branch to L
```

---

## 🔢 **Signed vs Unsigned Comparisons**

| **Comparison** | **Signed (`slt, slti`)** | **Unsigned (`sltu, sltui`)** |
| -------------- | ------------------------ | ---------------------------- |
| -1 vs 1        | `slt = 1` (True)         | `sltu = 0` (False)           |
| Max value      | `slt = 1` (True)         | `sltu = 0` (False)           |

Example:

```assembly
sltu $t0, $s0, $s1  # Compare unsigned numbers
```

---

## 🏗 **Register Usage in MIPS**

| Register    | Purpose                           |
| ----------- | --------------------------------- |
| `$a0 - $a3` | Arguments (Registers 4-7)         |
| `$v0, $v1`  | Return values (Registers 2-3)     |
| `$t0 - $t9` | Temporary registers (8-15, 24-25) |
| `$s0 - $s7` | Saved registers (16-23)           |
| `$gp`       | Global pointer (Register 28)      |
| `$sp`       | Stack pointer (Register 29)       |
| `$fp`       | Frame pointer (Register 30)       |
| `$ra`       | Return address (Register 31)      |

---

## 🔄 **Procedure Call Instructions**

### **Jump and Link (`jal`)**

```assembly
jal ProcedureLabel  # Save return address and jump
```

- Saves the return address in `$ra`.
- Jumps to `ProcedureLabel`.

### **Return from Procedure (`jr`)**

```assembly
jr $ra  # Return to caller
```

- Copies `$ra` to the **program counter**.
- Used for function returns and switch statements.
