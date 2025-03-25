# ⚙️ **Arithmetic for Computers** 🖥️💡

Computers perform arithmetic operations on **integers** and **floating-point numbers**, using specialized techniques to handle overflow, precision loss, and efficient multimedia processing.

Let's break it down! 🚀

---

## 🔢 **Integer Arithmetic: The Basics**

### ➕ **Integer Addition**

Computers use **binary addition**, just like we do with decimal numbers, but with only 0s and 1s.

💡 **Example:**

```
  0101   (5 in binary)
+ 0011   (3 in binary)
---------
  1000   (8 in binary) ✅
```

🔧 **Hardware Used:**

- **Half-Adder** – Adds two single-bit numbers.
- **Full-Adder** – Adds three bits (including carry-in).

---

### ➖ **Integer Subtraction**

Instead of direct subtraction, computers use **Two’s Complement**:

1. Take the **two's complement** of the number to be subtracted.
2. Add it like normal addition!

💡 **Example: 5 - 3 using two's complement**

1. Convert **3 to binary**: `0011`
2. Find its **two’s complement** (invert and add 1): `1101`
3. Perform addition:

```
  0101  (5 in binary)
+ 1101  (-3 in binary)
---------
  0010  (2 in binary) ✅
```

🎯 **Key Takeaway:** Subtraction is just **addition with the negative version** of a number!

---

## ⚠️ **Handling Overflow**

Overflow happens when the result **exceeds the available bits**.

🛠️ **Example:** If an 8-bit system adds `127 + 1`, the result **wraps around** and becomes `-128` instead of `128`.

### 🚨 **How different systems handle overflow?**

- **C, Java:** Ignore overflow (default behavior).
- **Ada, Fortran:** Raise an **exception** when overflow occurs.
- **MIPS Assembly:**
  - `addu, subu` → No exceptions 🚀
  - `add, sub` → Trigger an exception ❌

👀 **When an overflow occurs:**  
1️⃣ An **exception handler** is invoked.  
2️⃣ The **Exception Program Counter (EPC)** stores the faulty instruction.  
3️⃣ The system jumps to an **overflow handler** for recovery.

🛠️ **Think of it as an unscheduled emergency call!** 📞

---

# 🎥 **Arithmetic for Multimedia Processing** 🎧🎥

Modern computers optimize **video, audio, and image processing** using **SIMD (Single Instruction, Multiple Data)** techniques.

🛠️ **Techniques Used:**  
✅ **Parallel Computation** – Operate on multiple small values **simultaneously** using **64-bit registers**.  
✅ **Saturating Arithmetic** – Instead of **overflowing**, the result is **clamped** to the max/min value.

💡 **Example:**

- 🎵 **Audio Clipping** – Prevents sound distortion.
- 🎨 **Video Color Correction** – Stops color values from overflowing.

---

## ✖️ **Multiplication in Computers**

### **🔄 Binary Multiplication Example**

Multiplication in binary works similarly to decimal multiplication but only uses 0s and 1s.

💡 **Example: 3 × 5 (011 × 101 in binary)**

```
     011   (3 in binary)
  ×  101   (5 in binary)
  ---------
     011    (3 × 1)
    000     (3 × 0, shifted)
 + 011      (3 × 1, shifted)
  ---------
   1111    (15 in binary) ✅
```

---

## ➗ **Binary Division & MIPS Division**

Computers use **binary long division** for division.

💡 **Example: 11 ÷ 2 (1011 ÷ 10 in binary)**

```
  10 | 1011  (Divide 1011 by 10)
     - 10
      ------
       01    (Bring down the next bit)
       10   (10 fits in 10 once)
     - 10
      ------
        1  (Remainder)
```

📌 **Quotient = `101` (5 in decimal), Remainder = `1`**

---

### **MIPS Division in Assembly** 🏗️

💡 **MIPS uses two special registers:**

- **Hi:** Stores remainder
- **Lo:** Stores quotient

🛠️ **Instructions:**

```assembly
div rs, rt     # rs ÷ rt, stores quotient in Lo, remainder in Hi
mflo $t0       # Move quotient from Lo to $t0
mfhi $t1       # Move remainder from Hi to $t1
```

🔹 **No built-in overflow/divide-by-zero checks!** Must handle manually.

---

# 📊 **Floating-Point Arithmetic (IEEE 754)**

Computers use **floating-point numbers** to represent real numbers.

💡 **Format:**

```
Sign | Exponent | Mantissa
```

- **Sign Bit (S):** 0 for positive, 1 for negative.
- **Exponent (E):** Determines the magnitude.
- **Mantissa (M):** Stores the actual number.

---

## 🔢 **Floating-Point Addition**

### **Steps:**

1️⃣ Align exponents by shifting the smaller number.  
2️⃣ Perform addition on the mantissas.  
3️⃣ Normalize the result (adjust exponent back).

💡 **Example:** `1.1 × 10³ + 2.3 × 10²`  
1️⃣ Convert to same exponent: `1.1 × 10³ + 0.23 × 10³`  
2️⃣ Add mantissas: `1.1 + 0.23 = 1.33`  
3️⃣ Normalize: `1.33 × 10³` ✅

---

## 🛠️ **Floating-Point Multiplication**

### **Steps:**

1️⃣ Multiply mantissas.  
2️⃣ Add exponents.  
3️⃣ Normalize the result.

💡 **Example:**

```
(1.1 × 10³) × (2.0 × 10²)
= (1.1 × 2.0) × 10^(3+2)
= 2.2 × 10⁵ ✅
```

---

# ⚡ **Additional Insights & Practical Aspects**

## 🏎️ **Optimizing Arithmetic for Performance**

### 1️⃣ **Hardware Optimizations**

Computers optimize arithmetic using:  
✅ **Pipelining** – Breaks complex operations into smaller steps for parallel execution.  
✅ **Carry Lookahead Adders** – Speeds up addition by predicting carry values.  
✅ **Vector Processing** – SIMD (Single Instruction, Multiple Data) allows operations on multiple values at once.

💡 **Real-World Use Case:** **Modern CPUs (Intel, ARM) use vector registers like AVX and SSE to accelerate graphics and AI computations!** 🚀

---

## 🛠️ **Right-Shift Division & Arithmetic Shifts**

Right shifts (`>>`) are commonly used for **fast division** by powers of 2.

💡 **Example: Dividing by 2 using right shift**

```
10 (decimal) = 1010 (binary)
10 >> 1 = 0101 (binary) = 5 (decimal) ✅
```

🔹 **Logical Shift (`>>`)** – Fills with zeros.  
🔹 **Arithmetic Shift (`>>`)** – Preserves sign bit (for signed division).

📌 **When NOT to use it?** Right shifts don’t work for all cases (e.g., when precision matters).

---

## 🎯 **Floating-Point Rounding & Precision Issues**

### 1️⃣ **Why Can't Computers Represent Some Numbers Exactly?**

Floating-point numbers are limited by **finite bits**, meaning they **can't store some decimals exactly**.

💡 **Example:** `0.1` in decimal = `0.0001100110011...` (infinite binary fraction)  
🔹 The result? **Rounding errors!**

### 2️⃣ **Types of Rounding:**

✅ **Round to Nearest (default)** – Used in most CPUs.  
✅ **Truncation (chop extra bits)** – Faster but less accurate.  
✅ **Banker’s Rounding** – Rounds halfway cases to the nearest even number.

💡 **Real-World Example:**

- When dealing with **money**, rounding errors can cause small financial discrepancies!
- **Solution?** Use **arbitrary-precision libraries** (e.g., Python's `decimal` module).

---

## 🎭 **Edge Cases & Gotchas in Arithmetic**

1️⃣ **Integer Overflow in Real Life**  
💡 In 2012, a **video game bug** in _Fallout: New Vegas_ caused character health to **wrap around** when healing past max HP, making them **instantly die** instead! 💀

2️⃣ **Division by Zero: What Happens?**

- **Integers:** Usually crash the program (`Divide by zero exception`).
- **Floating-point:** Returns **Infinity (∞)** or **NaN (Not a Number)**.

3️⃣ **Floating-Point Comparisons Can Be Tricky!**

```c
float a = 0.1;
if (a == 0.1) {
    printf("Equal!");
} else {
    printf("Not Equal!");
}
```

💡 This may print **"Not Equal!"** due to **precision errors!** 😲  
🔹 **Fix?** Use `fabs(a - 0.1) < 0.00001` instead of direct comparison.

---

## 🎮 **Bonus: Arithmetic in Game Development & AI**

1️⃣ **Fixed-Point Arithmetic in Games** 🎮

- Some **old-school game consoles (e.g., PlayStation 1)** used **fixed-point numbers** instead of floating-point to save processing power.
- **Example:** Instead of `1.5`, store it as `15` and assume **1 decimal place**.

2️⃣ **Neural Networks & Floating-Point Math** 🤖

- AI models rely heavily on **matrix multiplications**, which use **floating-point optimizations (FP16, BF16, and FP32)** for speed and accuracy.
- **TensorFlow & PyTorch** optimize FP calculations using **special hardware (TPUs, GPUs).**

---

# 🔥 **Final Takeaways**

✔ **Binary arithmetic is the foundation of all computer calculations.**  
✔ **Overflow, rounding errors, and floating-point precision must be handled carefully.**  
✔ **Right shifts offer fast division but are limited.**  
✔ **Floating-point comparisons can be misleading—always use tolerances!**  
✔ **Optimized arithmetic is crucial for performance in games, AI, and multimedia.**
