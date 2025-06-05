# 📝 Week 11 Assignment — _Pipeline Hazards & Forwarding Magic_ ⚙️✨

> _Let's explore how instructions interact in the pipeline... and what magical delays we must prevent\~!_ 💫

---

## 🔍 Instruction Sequence

```assembly
or r1, r2, r3
or r2, r1, r4
or r1, r1, r2
```

---

## 🌟 4.9.1 — Dependences and Their Types

Let’s classify the data dependences between instructions\~ 🧠✨

### ✅ RAW (Read After Write) — _True Dependence_

- r1: Instruction 1 → Instruction 2
- r1: Instruction 1 → Instruction 3
- r2: Instruction 2 → Instruction 3

### 🚫 WAR (Write After Read) — _Anti-Dependence_

- r2: Instruction 1 → Instruction 2
- r1: Instruction 2 → Instruction 3

### ❌ WAW (Write After Write) — _Output Dependence_

- r1: Instruction 1 → Instruction 3

🧙‍♀️ These dependences can cause hazards during pipelined execution if not handled properly!

---

## ⚠️ 4.9.2 — No Forwarding: Insert NOPs for Hazard Removal

Without any forwarding, the processor must **stall** to wait for operands. So we insert `nop` instructions to prevent incorrect execution.

```assembly
or r1, r2, r3
nop
nop
or r2, r1, r4
nop
nop
or r1, r1, r2
```

🔧 Explanation:

- Between 1st and 2nd `or`: 2-cycle stall (waiting for r1)
- Between 2nd and 3rd `or`: 2-cycle stall (waiting for r2 and r1)

😵 Total 4 NOPs just to play it safe...

---

## 🛡️ 4.9.3 — Full Forwarding: Hazards Eliminated Smoothly

With **full forwarding**, data can be passed directly from one pipeline stage to another — like a magical relay\~ ✨

No stalls are needed here:

```assembly
or r1, r2, r3
or r2, r1, r4
or r1, r1, r2
```

✨ ALU results are forwarded from EX stage to the next EX stage. Since all instructions are `or` (ALU-type), **no delays or stalls** are required.

---

## ⏱️ 4.9.4 — Execution Time & Speedup

Let’s calculate how much faster we get with forwarding\~

### ⌛ Without Forwarding

```assembly
or r1, r2, r3
nop
nop
or r2, r1, r4
nop
nop
or r1, r1, r2
```

- Total instructions: 3 + 4 nops = 7
- Pipeline depth = 5 stages
- Total cycles = 7 + (5 - 1) = 11
- Cycle time = 250 ps
- 🕒 Execution time = 11 x 250 = **2750 ps**

---

### ⚡ With Full Forwarding

```assembly
or r1, r2, r3
or r2, r1, r4
or r1, r1, r2
```

- Total instructions = 3
- Pipeline depth = 5 stages
- Total cycles = 3 + (5 - 1) = 7
- Cycle time = 300 ps
- 🕒 Execution time = 7 x 300 = **2100 ps**

---

### 🏎️ Speedup from Forwarding

```
Speedup = Time (No Forwarding) / Time (Full Forwarding)
        = 2750 / 2100
        = 1.31
```

💡 **Result**: Full forwarding gives us a **31% speedup**\~ Woohoo! 🥳📈
