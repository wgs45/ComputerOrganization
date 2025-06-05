# 🏰✨ Week 10 Assignment: Pipelining Magic ✨⏱️

> _“Even the swiftest CPU must obey the rhythm of the clock… but with pipelining, we make every tick count!”_ ⚡🕰️

---

## 📖 Problem Statement

We analyze how pipelining changes the processor’s clock cycle time and instruction latencies.
Given the following stage latencies:

| Stage | IF    | ID    | EX    | MEM   | WB    |
| ----- | ----- | ----- | ----- | ----- | ----- |
| Time  | 250ps | 350ps | 150ps | 300ps | 200ps |

Instruction mix (percentages):

| Instruction | ALU | BEQ | LW  | SW  |
| ----------- | --- | --- | --- | --- |
| Frequency   | 45% | 20% | 20% | 15% |

Answer the following:

1. **(4.8.1)** What is the clock cycle time in a pipelined vs. non-pipelined processor?
2. **(4.8.2)** What is the total latency of an LW instruction in pipelined vs. non-pipelined?
3. **(4.8.3)** If we can split one pipeline stage into two equal sub-stages, which stage should we split, and what is the new clock cycle time?
4. **(4.8.4)** Assuming no stalls/hazards, what is the utilization of the data memory?
5. **(4.8.5)** Assuming no stalls/hazards, what is the utilization of the write-port of the register file?

---

## 1️⃣ 4.8.1: Clock Cycle Time Comparison

### 🔴 Non-Pipelined Processor

- **Formula**: Sum of all stage latencies

Total time = IF + ID + EX + MEM + WB

- **Calculation**:

Total time = 250 + 350 + 150 + 300 + 200 = 1250 ps

> 🔔 **Result**:
> **Non-Pipelined Cycle Time = 1250 ps**

---

### 🔵 Pipelined Processor

- **Principle**: Each pipeline stage must fit within one clock cycle → the slowest (longest) stage dictates the clock.
- **Find the maximum stage latency**:

Max{250,350,150,300,200} = 350 ps

> 🔔 **Result**:
> **Pipelined Cycle Time = 350 ps**

---

### 🧚‍♀️ TL;DR (4.8.1)

- Non-pipelined: **1250 ps**
- Pipelined: **350 ps**

---

## 2️⃣ 4.8.2: LW Instruction Latency

### 🔴 Non-Pipelined Processor

▷ **Every stage runs sequentially** → total latency = sum of all five stages (as in 4.8.1).

Total latency = IF + ID + EX + MEM + WB

> **Non-Pipelined LW Latency = 1250 ps**

---

### 🔵 Pipelined Processor

▷ **LW must still traverse all five stages**, but each stage takes one cycle (350 ps).

Total latency = 250 + 350 + 150 + 300 + 200 = 1250 ps

> **Pipelined LW Latency = 1750 ps**

---

### 🧚‍♀️ TL;DR (4.8.2)

- Non-pipelined LW: **1250 ps**
- Pipelined LW: **1750 ps**

_N.B._: Pipelining increases _per-instruction_ latency slightly (due to slowest stage), but boosts overall throughput when many instructions flow through the pipeline! 🌪️✨

---

## 3️⃣ 4.8.3: Splitting a Bottleneck Stage

We may split the longest pipeline stage into two equal halves, reducing the critical-path delay.

| Stage Latencies              |
| ---------------------------- |
| IF = 250 ps                  |
| **ID = 350 ps** ← bottleneck |
| EX = 150 ps                  |
| MEM = 300 ps                 |
| WB = 200 ps                  |

### 🔮 Which Stage to Split?

- The **ID stage** (350 ps) is longest → splitting yields two sub-stages of 175 ps each.

---

### ✂️ After Splitting ID into ID₁ & ID₂

| Stage | IF    | ID₁   | ID₂   | EX    | MEM   | WB    |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| Time  | 250ps | 175ps | 175ps | 150ps | 300ps | 200ps |

- **New maximum stage latency** = max{250, 175, 175, 150, 300, 200} = **300 ps** (MEM stage).

> ✨ **New Pipelined Cycle Time = 300 ps**

---

### 🧚‍♀️ TL;DR (4.8.3)

- **Split**: ID (350 ps) → ID₁ (175 ps) + ID₂ (175 ps)
- **New slowest stage**: MEM (300 ps)
- **New cycle time**: **300 ps**

---

## 4️⃣ 4.8.4: Data Memory Utilization

Which instructions access data memory?

- **LW (loads)** → _reads_ from data memory
- **SW (stores)** → _writes_ to data memory
- ALU & BEQ do **NOT** access data memory.

Given instruction mix:

- LW = 20%
- SW = 15%
- (ALU 45%, BEQ 20% do not use data memory)

**Utilization** = P(LW) + P(SW)

Utilization = 20% + 15% = 35%

> **Data Memory Utilization = 35%**

---

## 5️⃣ 4.8.5: Register Write-Port Utilization

Which instructions write to the register file?

- **ALU instructions** (45%) → write ALU result back
- **LW instructions** (20%) → write loaded data back
- BEQ (20%) & SW (15%) **do not** write to registers.

**Utilization** = P(ALU) + P(LW)

Utilization = 45% + 20% = 65%

> **Register Write-Port Utilization = 65%**

---

## 🌸 Final Sparkle Summary ✨

1. **Clock Cycle Times (4.8.1)**

   - Non-Pipelined = **1250 ps**
   - Pipelined = **350 ps**

2. **LW Latency (4.8.2)**

   - Non-Pipelined = **1250 ps**
   - Pipelined = **1750 ps**

3. **Splitting the Bottleneck (4.8.3)**

   - Split **ID (350 ps)** → two × 175 ps
   - New slowest = **MEM (300 ps)**
   - New cycle time = **300 ps**

4. **Data Memory Utilization (4.8.4)** = **35%**
   _(Only LW + SW access data memory)_

5. **Register Write-Port Utilization (4.8.5)** = **65%**
   _(Only ALU + LW write back to registers)_
