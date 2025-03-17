# ⚙️ **Arithmetic for Computers**

Computers perform arithmetic operations on **integers** and **floating-point numbers**, handling overflow and multimedia processing efficiently through specialized instructions and techniques.

---

## 🔢 **Integer Arithmetic**

### ➕ **Integer Addition**

- Follows **binary arithmetic** rules.
- Uses **half-adders** and **full-adders** in hardware.

### ➖ **Integer Subtraction**

- Uses **two's complement** representation:  
  A - B = A + (-B)
  where –B is the **two’s complement** of B.

### ⚠️ **Dealing with Overflow**

Overflow happens when the result **exceeds the number of available bits**.

**Handling overflow in programming languages:**

- ✅ **C, Java** – Ignore overflow (default behavior).
- ✅ **Ada, Fortran** – Raise an **exception** when overflow occurs.

**Handling overflow in MIPS Assembly:**

- **`addu, addui, subu`** – No overflow exceptions.
- **`add, addi, sub`** – Cause overflow exceptions.

**What happens when an overflow occurs?**

1. Exception **handler** is invoked.
2. The **exception program counter (EPC)** saves the instruction address.
3. Control jumps to a **predefined handler** for corrective action.

🛠️ **Exception = Unscheduled Procedure Call!**

---

## 🎥 **Arithmetic for Multimedia Processing**

Multimedia operations deal with **8-bit and 16-bit** data vectors using **64-bit adders** and **partitioned carry chains** for parallel computation.

### ✅ **Techniques Used:**

- **SIMD (Single Instruction, Multiple Data)** – Performs the same operation on multiple data points.
- **Saturating operations** – Instead of wrapping around on overflow, results are clamped to the **maximum representable value**.

### 📺 **Applications:**

- 🎧 **Audio Processing** – Clipping audio signals.
- 🎥 **Video Processing** – Saturation to prevent color distortion.

---

## ✖️ **Multiplication in Computers**

Multiplication is handled using **binary arithmetic**, optimized through special algorithms.

### 🎯 **Multiplication Methods:**

- **Shift-and-Add Method** – Basic binary multiplication.
- **Booth’s Algorithm** – Efficient for signed numbers.
- **Wallace Tree Multipliers** – Fast parallel addition of partial products.

### 🔄 **Binary Multiplication Example**

**Multiplying 3 × 5 (011 × 101 in binary):**

```
     011   (3 in binary)
  ×  101   (5 in binary)
  ---------
     011    (3 × 1)
    000     (3 × 0, shifted)
 + 011      (3 × 1, shifted)
  ---------
   1111    (15 in binary)
```

🔑 **Final Result = 15 (Decimal)!**

---

## 📊 **Floating-Point Arithmetic**

Floating-point numbers approximate real numbers using **IEEE 754 standard** representation.

### **Representation Format:**

A floating-point number consists of:

- **Sign Bit (S)** – 1 for negative, 0 for positive.
- **Exponent (E)** – Adjusts the magnitude.
- **Mantissa (M)** – Stores the significant digits.

### **Floating-Point Operations:**

- **Addition & Subtraction** – Align exponents before performing arithmetic.
- **Multiplication & Division** – Multiply/divide mantissas and adjust exponents.

### **Common Issues:**

- **Precision Loss** – Due to limited mantissa bits.
- **Underflow & Overflow** – When numbers are too small or large to represent.
