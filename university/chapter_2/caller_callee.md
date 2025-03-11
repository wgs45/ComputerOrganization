# 📞 Caller & 📟 Callee in MIPS

---

## 🚀 What Are Caller & Callee?

- **Caller**: The function that **calls** another function.
- **Callee**: The function that **gets called** by the caller.

### 🔄 How It Works

1️⃣ **Caller:**

- Puts parameters in **$a0 - $a3** 🏷️
- Jumps to callee using **`jal X`** 🚀

2️⃣ **Callee:**

- Performs computations 🧮
- Stores results in **$v0 - $v1** ✅
- Returns to caller using **`jr $ra`** 🔁

3️⃣ **Caller Resumes Execution** 📌

- Continues from **`$ra`** (Return Address)

🔹 **Extra Info:**

- The **Program Counter (PC)** stores the current instruction.
- `jal` saves `PC + 4` into `$ra` before jumping.

---

## 🎯 Using More Registers Efficiently

- `$t0 - $t9` ➝ Temporary registers **(not saved by callee)** ⚡
- `$s0 - $s7` ➝ Saved registers **(must be saved & restored by callee)** 💾

### ⏳ Why?

To avoid unnecessary saving/restoring of registers that aren't used! 🏋️‍♂️

---

## 🍃 Leaf Procedures (No Function Calls Inside)

### 📝 C Code

```c
int leaf_example(int g, int h, int i, int j) {
    int f;
    f = (g + h) - (i + j);
    return f;
}
```

### 🏗️ MIPS Assembly

```assembly
leaf_example:
    # Save $s0 (since it's a saved register)
    addi $sp, $sp, -4
    sw $s0, 0($sp)

    # Perform calculations 🧮
    add $t0, $a0, $a1    # t0 = g + h
    add $t1, $a2, $a3    # t1 = i + j
    sub $s0, $t0, $t1    # s0 = (g + h) - (i + j)

    # Store result in $v0 for return
    add $v0, $s0, $zero

    # Restore $s0 and return 🔄
    lw $s0, 0($sp)
    addi $sp, $sp, 4
    jr $ra
```

📌 **Key Takeaways:**

- **Arguments:** Stored in `$a0 - $a3` 🎒
- **Result:** Stored in `$v0` 🏆
- **Leaf procedures**: Functions that **don’t call** other functions 🌱

---

## 🌳 Non-Leaf Procedures (Calling Another Function)

### 📝 C Code

```c
int fact(int n) {
    if (n < 1) return 1;
    else return n * fact(n - 1);
}
```

### 🏗️ MIPS Assembly

```assembly
fact:
    addi $sp, $sp, -8    # Make space for return address & argument
    sw $ra, 4($sp)       # Save return address 📌
    sw $a0, 0($sp)       # Save argument n 📥

    slti $t0, $a0, 1     # if (n < 1) ?
    beq $t0, $zero, L1   # If false, go to L1 🚦

    # Base case: return 1 🎯
    addi $v0, $zero, 1   # Return value = 1
    addi $sp, $sp, 8     # Restore stack 🧹
    jr $ra               # Return to caller

L1:
    addi $a0, $a0, -1    # n - 1 (recursive call)
    jal fact             # Call fact(n - 1) 🔄

    lw $a0, 0($sp)       # Restore original n
    lw $ra, 4($sp)       # Restore return address
    addi $sp, $sp, 8     # Restore stack

    mul $v0, $a0, $v0    # n * fact(n - 1) 🏗️
    jr $ra               # Return
```

📌 **Key Takeaways:**

- **Recursion requires stack management** 📚
- **Must save return address & arguments** before calling another function 🛑
- **Restore everything** before returning 🔄
