# **🔥 MIPS Arithmetic Cheat Sheet 🔥**

## **📌 Basic Arithmetic Instructions**

| Instruction        | Operation            | Example              | Description                             |
| ------------------ | -------------------- | -------------------- | --------------------------------------- |
| `add rd, rs, rt`   | Addition             | `add $t0, $t1, $t2`  | `$t0 = $t1 + $t2` (with overflow check) |
| `addu rd, rs, rt`  | Unsigned Addition    | `addu $t0, $t1, $t2` | `$t0 = $t1 + $t2` (no overflow check)   |
| `addi rd, rs, imm` | Immediate Addition   | `addi $t0, $t1, 10`  | `$t0 = $t1 + 10`                        |
| `sub rd, rs, rt`   | Subtraction          | `sub $t0, $t1, $t2`  | `$t0 = $t1 - $t2` (with overflow check) |
| `subu rd, rs, rt`  | Unsigned Subtraction | `subu $t0, $t1, $t2` | `$t0 = $t1 - $t2` (no overflow check)   |

---

## **✖️ Multiplication & Division**

| Instruction      | Operation         | Example             | Description                                   |
| ---------------- | ----------------- | ------------------- | --------------------------------------------- |
| `mul rd, rs, rt` | Multiplication    | `mul $t0, $t1, $t2` | `$t0 = $t1 * $t2`                             |
| `mult rs, rt`    | Multiply (Hi/Lo)  | `mult $t1, $t2`     | Stores result in **Hi/Lo registers**          |
| `multu rs, rt`   | Unsigned Multiply | `multu $t1, $t2`    | Same as `mult`, but unsigned                  |
| `mfhi rd`        | Move from Hi      | `mfhi $t0`          | Moves **high bits** of `mult` result to `$t0` |
| `mflo rd`        | Move from Lo      | `mflo $t0`          | Moves **low bits** of `mult` result to `$t0`  |
| `div rs, rt`     | Division          | `div $t1, $t2`      | Quotient in **Lo**, remainder in **Hi**       |
| `divu rs, rt`    | Unsigned Division | `divu $t1, $t2`     | Same as `div`, but unsigned                   |

💡 **Accessing Division Results:**

```assembly
div $t1, $t2
mflo $t0  # $t0 = Quotient
mfhi $t1  # $t1 = Remainder
```

---

## **🛠️ Logical & Shift Operations**

| Instruction         | Operation              | Example             | Description                       |
| ------------------- | ---------------------- | ------------------- | --------------------------------- | ----- |
| `and rd, rs, rt`    | AND                    | `and $t0, $t1, $t2` | `$t0 = $t1 & $t2`                 |
| `or rd, rs, rt`     | OR                     | `or $t0, $t1, $t2`  | `$t0 = $t1                        | $t2`  |
| `xor rd, rs, rt`    | XOR                    | `xor $t0, $t1, $t2` | `$t0 = $t1 ^ $t2`                 |
| `nor rd, rs, rt`    | NOR                    | `nor $t0, $t1, $t2` | `$t0 = ~($t1                      | $t2)` |
| `sll rd, rt, shamt` | Logical Shift Left     | `sll $t0, $t1, 2`   | `$t0 = $t1 << 2`                  |
| `srl rd, rt, shamt` | Logical Shift Right    | `srl $t0, $t1, 2`   | `$t0 = $t1 >> 2` (fills with 0s)  |
| `sra rd, rt, shamt` | Arithmetic Shift Right | `sra $t0, $t1, 2`   | `$t0 = $t1 >> 2` (keeps sign bit) |

💡 **Shift Operations in Action:**

```assembly
# Divide by 4 using arithmetic shift
sra $t0, $t1, 2   # $t0 = $t1 / 4 (preserves sign)
```

---

## **🔢 Floating-Point Instructions (MIPS FP Coprocessor - `FPU`)**

| Instruction           | Operation                   | Example               | Description                       |
| --------------------- | --------------------------- | --------------------- | --------------------------------- |
| `lwc1 ft, offset(rs)` | Load Word to FP Register    | `lwc1 $f0, 0($t1)`    | Load float from memory            |
| `swc1 ft, offset(rs)` | Store Word from FP Register | `swc1 $f0, 0($t1)`    | Store float to memory             |
| `add.s fd, fs, ft`    | FP Addition (Single)        | `add.s $f0, $f1, $f2` | `$f0 = $f1 + $f2`                 |
| `sub.s fd, fs, ft`    | FP Subtraction (Single)     | `sub.s $f0, $f1, $f2` | `$f0 = $f1 - $f2`                 |
| `mul.s fd, fs, ft`    | FP Multiplication           | `mul.s $f0, $f1, $f2` | `$f0 = $f1 * $f2`                 |
| `div.s fd, fs, ft`    | FP Division                 | `div.s $f0, $f1, $f2` | `$f0 = $f1 / $f2`                 |
| `c.eq.s fs, ft`       | Compare Equal               | `c.eq.s $f0, $f1`     | Sets flag if `$f0 == $f1`         |
| `bc1t label`          | Branch if True              | `bc1t LABEL`          | Branches if FP comparison is true |

💡 **Example: Floating-Point Addition in MIPS**

```assembly
lwc1 $f0, 0($t1)   # Load float from memory
lwc1 $f1, 4($t1)
add.s $f2, $f0, $f1  # $f2 = $f0 + $f1
swc1 $f2, 8($t1)   # Store result back
```

---

## **🚀 Tips & Tricks for MIPS Arithmetic**

💡 **Avoid Integer Overflow in Assembly:**

- Use **`addu`, `subu`** instead of `add`, `sub` if overflow doesn’t matter.
- Perform **manual range checking** if necessary.

💡 **Optimize Division Using Bitwise Shifts:**

- Instead of `div $t0, $t1, 2`, use `sra $t0, $t1, 1` for efficiency.

💡 **Floating-Point Operations Must Use `FPU` Instructions:**

- Use `lwc1` and `swc1` for memory operations.
- Always perform **exponent alignment** before adding FP numbers!

---

# **✨ Final Takeaways ✨**

✔ **Mastering MIPS arithmetic helps with low-level programming & CPU architecture.**  
✔ **Use `Hi/Lo` registers for multiplication & division results.**  
✔ **Shifting operations (`sll`, `sra`, `srl`) can speed up computations.**  
✔ **Floating-point operations require `FPU` instructions (`add.s`, `mul.s`).**
