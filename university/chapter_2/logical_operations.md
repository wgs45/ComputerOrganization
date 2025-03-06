# 🌟 **MIPS Syntax Guide**

MIPS (Microprocessor without Interlocked Pipeline Stages) is a **RISC architecture** where you work with low-level instructions.

---

## 🔲 **Logical Operations**

Logical operations are essential for **bitwise manipulations**. These operations let you interact with individual bits of data, which is crucial for low-level programming.

| **Operation**   | **C** | **Java** | **MIPS**      |
| --------------- | ----- | -------- | ------------- |
| **Shift Left**  | `<<`  | `<<`     | `sll`         |
| **Shift Right** | `>>`  | `>>`     | `srl`         |
| **Bitwise AND** | `&`   | `&`      | `and`, `andi` |
| **Bitwise OR**  |       |          | `or`, `ori`   |
| **Bitwise NOT** | `~`   | `~`      | `nor`         |

- **Shift operations**: Useful for manipulating groups of bits.
- **AND operations**: Mask specific bits by selecting and clearing others to 0.
- **OR operations**: Change 0s to 1s and vice versa. Also, `NOR` helps to invert the bits.

---

## 🔁 **Shift Operations**

Shift operations work by **moving bits left or right**, with the flexibility of filling the vacated positions with zeros. This is useful for multiplication and division by powers of 2. 🚀

| 🔢 **op** (6 bits) | 🔢 **rs** (5 bits) | 🔢 **rt** (5 bits) | 🔢 **rd** (5 bits) | 🔢 **shamt** (5 bits) | 🔢 **funct** (6 bits) |
| ------------------ | ------------------ | ------------------ | ------------------ | --------------------- | --------------------- |

- **`shamt`**: This tells you how many **positions** to shift (the shift amount).
- **Shift Left Logical (`sll`)**:
  - Shifts **left** and fills the vacated bits with **0s**.
  - **Effect**: Shift left by **i** bits = multiply by **2^i**.
  - Example: `sll $t0, $t1, 2` (Multiply `$t1` by 4 and store in `$t0`).
- **Shift Right Logical (`srl`)**:
  - Shifts **right** and fills with **0s**.
  - **Effect**: Shift right by **i** bits = divide by **2^i** (for **unsigned numbers**).
  - Example: `srl $t0, $t1, 2` (Divide `$t1` by 4 and store in `$t0`).

---

## 🛠️ **AND Operations**

The **AND** operation is great for **masking** certain bits in a word, allowing you to select specific bits while clearing others. It’s like having a **bit-filtering tool**! 🧰

### 🔑 Key Points

- **Select bits** while clearing others to **0**.
- **Mask** "conceals" the bits you're not interested in.

```assembly
and $t0, $t1, $t2  # Performs $t0 = $t1 & $t2
```

This instruction stores the result of the bitwise AND between registers `$t1` and `$t2` in `$t0`. 💡

---

## 🔄 **OR Operations**

The **OR** operation is used to **invert** bits. It flips 0 to 1 and 1 to 0. Think of it like a **toggle switch**! 🔄

- **MIPS has a powerful instruction called `NOR`**:
  - **a NOR b** = **NOT (a OR b)**.
  - **a NOR 0** = **NOT (a OR 0)** = **NOT a**.  
    This is a **3-operand instruction**!

```assembly
nor $t0, $t1, $zero  # $t0 = NOT $t1 (bitwise negation)
```

This example takes the **bitwise negation** of `$t1` and stores it in `$t0`. So, it **inverts** every bit in `$t1`! 🔥

---

## ⚖️ **Conditional Operations**

Conditional operations allow you to **branch** to a specific instruction depending on whether a condition is true or false. It’s like **decision-making** in programming! 💡

1. **Branch if Equal (BEQ)**:

   ```assembly
   beq $t0, $t1, L1  # if ($t0 == $t1) branch to L1
   ```

   - If the contents of registers `$t0` and `$t1` are **equal**, jump to label `L1`.
   - Otherwise, continue with the next instruction.

2. **Branch if Not Equal (BNE)**:

   ```assembly
   bne $t0, $t1, L1  # if ($t0 != $t1) branch to L1
   ```

   - If `$t0` is **not equal** to `$t1`, jump to label `L1`.

3. **Unconditional Jump**:

   ```assembly
   j L1  # jump to L1 (always)
   ```

   - This is an **unconditional jump** that goes straight to `L1`.

---

## 🏃 **Jumping to Labels**

Sometimes you need to **move around in your code** with jumps. These jump instructions make your program more flexible and efficient. They allow you to skip around without following the usual sequential order! 🏃‍♂️💨

---

### ✨ **Quick Summary:**

- **Shift Operations (`sll`, `srl`)**: Move bits to the left or right for **multiplication** or **division**.
- **AND Operations**: Mask bits to clear or select them.
- **OR & NOR Operations**: Toggle bits and invert values.
- **Branching**: Jump to different code sections based on conditions, making your program **dynamic**.
