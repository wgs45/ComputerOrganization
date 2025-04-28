# 🌀 **Pipelining – Speed Up Like a Pro CPU** 🚀

---

## 🧼 Pipelined Laundry Analogy 👚👖

- **Parallel execution** = **Pipelining** 🌀
- ⏱️ 4 loads:
  - **Without pipelining**: `4 × 2 = 8 units`
  - **With pipelining**: `3.5 units`
  - ➡️ **Speedup ≈ 2.3x** ⚡
- **Non-stop washing**:
  - Speedup = `2n / (0.5n + 1.5) ≈ 4x` 💥

> ✅ **Takeaway**: Overlapping work → massive speedup 🔥

---

## 🧠 MIPS 5-Stage Pipeline 💡

1. **IF** – Instruction Fetch 🧾
2. **ID** – Instruction Decode & Register Read 🧠
3. **EX** – Execute / Address Calculation 🔢
4. **MEM** – Memory Access 📦
5. **WB** – Write Back to Register ✍️

> 📦 Every instruction passes through **all 5 stages**, one per clock cycle!

---

## ⏲️ Pipeline vs. Single-Cycle Timing

| Instruction | IF  | ID  | EX  | MEM | WB  | Total (Single-Cycle) |
| ----------- | --- | --- | --- | --- | --- | -------------------- |
| `lw`        | 200 | 100 | 200 | 200 | 100 | **800ps** 🐢         |
| `sw`        | 200 | 100 | 200 | 200 | —   | **700ps**            |
| `R-type`    | 200 | 100 | 200 | —   | 100 | **600ps**            |
| `beq`       | 200 | 100 | 200 | —   | —   | **500ps**            |

- ✅ **Pipelined Clock Time** = **200ps**
- ❌ **Single-Cycle Clock Time** = **800ps**

> 🔥 Ideal speedup ≈ 4x when pipelined perfectly!

---

## 🚀 How Pipelining Supercharges CPUs

- 🧠 Speedup = `Time_nonpipelined / Time_pipelined`
- If stages are balanced ➡️ Speedup ≈ **# of stages**
- ⚠️ **Real life**: stages aren't perfectly balanced = slightly less speedup 🐌
- 🎯 **Boosts throughput** (instructions per time), not single instruction latency!

---

## 🎯 Why MIPS Loves Pipelining 💖

- ✅ Uniform 32-bit instructions = fast fetch & decode 📏
- ✅ Few instruction formats = simpler pipeline 💨
- ✅ Memory only accessed by `lw/sw` ➡️ organized access 📦
- ✅ Word-aligned accesses = no weird address problems 🙅‍♀️

---

# ⚡ Pipeline Hazards – Your CPU's Worst Enemies

---

## 1️⃣ Structural Hazards 🛠️

- Conflict over shared resources (e.g., memory) 🚧
- ❗ **Solution**: Separate instruction and data memories or use **caches** 🧠
- 🫧 **Bubble** = pipeline **stall**

---

## 2️⃣ Data Hazards 🔗

- Instruction needs a **value before it's ready** 🔁

```assembly
add $s0, $t0, $t1
sub $t2, $s0, $t3  # Needs $s0 result!
```

#### 🔄 Solution: **Forwarding / Bypassing**

- Use the result **early**, not after it’s saved! 🦾
- **Can't time travel**: only forward _future ➡️ present_ 😅

---

### ⚡ Load-Use Hazard

```assembly
lw $t1, 20($t0)
add $t2, $t1, $t3  # $t1 not ready yet!
```

- ❌ Forwarding **won't help**: data isn’t ready!
- 🚦 Must insert **stalls**!

---

### 🏗️ Forwarding = Fast Rescue

- Use **internal results** before they hit the register file ✨
- Needs extra **forwarding paths** hardware 🦿
- 🚫 Don’t forward from $zero register!

---

## 3️⃣ Control Hazards 🎮

- Branch or jump ➡️ **don't know next instruction yet!** 🤷

#### Solutions

- Stall the pipeline (stall on branch) 🧱
- Branch prediction 🔮
- Delay slots ⏳

---

# 🎯 Beating Branch Hazards

---

### ❗ Stall on Branch

- Wait until branch is **resolved** before fetching next 🔄
- 🛠️ Hardware support needed: compare registers & compute branch address early

---

### 🔮 Branch Prediction

- **Predict not taken**: assume no branch ➡️ full speed 🏎️
- Stall only if prediction is wrong 🚦

---

### 🧠 Smarter Branch Prediction

- **Static**: predict based on behavior (e.g., backward loops = predict taken) 🔁
- **Dynamic**: record history & predict based on **past trends** 📈

---

### ⏳ Delayed Branch

- Always execute the next instruction before branching 🏃
- MIPS assembler rearranges instructions automatically! 🔄

---

# 🛠️ Pipelined Datapath Overview

---

## 🚏 Pipeline Registers

- Between each stage to **hold results** 🧳
  - **IF/ID → ID/EX → EX/MEM → MEM/WB**
- Think of them as **"mini-stations"** passing work to the next stage 🚂

---

## 🔍 Pipeline Operation

- **Cycle-by-cycle** movement 📈
- See how instructions overlap and flow 🌊
- Focus on **single-clock-cycle** diagrams for load & store 🖼️

---

# ⚡ Data Hazards in ALU Instructions

---

```assembly
sub $2, $1, $3
and $12, $2, $5
or $13, $6, $2
add $14, $2, $2
sw $15, 100($2)
```

### 🕵️ Hazard Detection

- `sub` ➡️ `and`: **EX hazard** (forward EX/MEM ➡️ ID/EX)
- `sub` ➡️ `or`: **MEM hazard** (forward MEM/WB ➡️ ID/EX)
- `sub` ➡️ `add/sw`: ✅ No hazard!

---

# 🔥 Hazard Detection & Forwarding Logic

---

- Pass register numbers down pipeline 📦
- Compare destination (Rd) with sources (Rs/Rt) 🔎

#### Forward when

- EX/MEM.RegisterRd == ID/EX.RegisterRs or ID/EX.RegisterRt
- MEM/WB.RegisterRd == ID/EX.RegisterRs or ID/EX.RegisterRt

---

# ⚡ Double Data Hazard

---

```assembly
add $1, $1, $2
add $1, $1, $3
add $1, $1, $4
```

- Both **EX and MEM hazards** at once ⚡
- Always use **latest value** for forwarding!

---

# 🎮 Special Case: Branch Hazards

---

- **Branch depends** on comparison results ➡️
- Resolve with **forwarding** if possible 🔁
- **1-2 stalls** needed if relying on **loads** before branch 🧱

---

### 🧠 Quick Fix

- Move branch outcome calculation **early** (in ID stage) 🏎️

---

# 🛡️ Summary: Pipeline Hazards Mastered

| Hazard Type   | Example                | Solution                |
| ------------- | ---------------------- | ----------------------- |
| Structural 🛠️ | Single memory conflict | Separate memory/caches  |
| Data 🔗       | Result needed early    | Forwarding & stalls     |
| Control 🎮    | Branch decision delay  | Prediction, delay slots |
