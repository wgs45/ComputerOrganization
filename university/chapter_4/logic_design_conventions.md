# ⚙️ **Logic Design Basics** 💡

---

## 🧠 **Core Concepts**

- Information is **encoded in binary**:
  - 🔌 Low Voltage = `0`
  - 🔋 High Voltage = `1`
- 🧵 **One wire per bit**
- 🧵🧵 **Multi-bit data** = multi-wire **buses**
- 🧮 **Combinational Elements**:
  - Outputs depend **only on current inputs**
- 🧷 **Sequential (State) Elements**:
  - Store **information**
  - Outputs depend on **inputs + past states**

---

## 🔄 **Combinational Elements**

These elements perform operations **instantly** based on current inputs. No memory or history is involved.

### 🔹 AND Gate

🧮 Logic: `Y = A & B`

|  A  |  B  |  Y  |
| :-: | :-: | :-: |
|  0  |  0  |  0  |
|  0  |  1  |  0  |
|  1  |  0  |  0  |
|  1  |  1  |  1  |

---

### 🔀 Multiplexer (MUX)

🧮 Logic: `Y = S ? I1 : I0`

📦 A selection box:

- **Select line (S)** decides whether to pass **I0** or **I1** to output **Y**

```
    I0 ─────┐
            ├── Y
    I1 ─────┘
           ↑
           S (select)
```

---

### ➕ Adder

🧮 Logic: `Y = A + B`

- Adds two binary numbers
- Often part of ALUs or counters

---

### 🧠 Arithmetic Logic Unit (ALU)

🧮 Logic: `Y = F(A, B)`

- Can perform multiple operations: `add`, `sub`, `and`, `or`, `slt`, etc.
- Controlled by a **function selector (F)**

Think of it as the **math brain 🧠** of your CPU!

---

## 🕓 **Sequential Elements**

These **store data** and are controlled by a **clock** ⏰.

### 🔹 Register

- Stores **1 word** of data
- **Updates only** on a **clock edge** (0 ➡ 1)
- Basic building block for memory!

```
    D ─────▶│Register│─────▶ Q
           │   ↑    │
         Clock Edge (↑)
```

---

### ✍️ Register with **Write Control**

- Adds a **Write Enable** input 🖊️
- Only updates **when Write = 1**

```
         Write = 1
            │
    D ─────▶│Register│─────▶ Q
           │   ↑    │
         Clock Edge (↑)
```

Used in **memory**, **register files**, or when **conditional updates** are required.

---

## 🕰️ **Clocking Methodology**

🔁 Defines when signals can be **read or written**

- **Combinational logic** happens **between** clock edges
- **State elements (e.g., registers)**:
  - Read at **beginning**
  - Written at **end**

### ⏳ Clock Period

⏱️ Determined by **longest delay** in the combinational path (also called the **critical path**)

> ⚠️ A **race condition** could happen if data is read and written at the wrong times!  
> ✅ Edge-triggered designs help prevent this by clearly defining **read/write windows**

---

## 🧰 Summary Table

| 🔧 Element        | 💬 Description            | 🕒 Memory? |
| ----------------- | ------------------------- | ---------- |
| AND Gate          | Logical AND               | ❌         |
| Multiplexer       | Selects between inputs    | ❌         |
| Adder             | Binary addition           | ❌         |
| ALU               | Performs logic/arithmetic | ❌         |
| Register          | Stores data (clocked)     | ✅         |
| Register w/ Write | Conditionally stores data | ✅         |
