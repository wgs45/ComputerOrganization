# 🌀 **Pipelining – Speed Up Like a Pro CPU** 🚀

---

### 🧼 Pipelined Laundry Analogy 👚👖

- Do multiple loads **in parallel** = **Pipelining**
- ⏱️ Total time with 4 loads:
  - **Non-pipelined**: `4 * 2 = 8 units`
  - **Pipelined**: `3.5 units`
  - \*\*Speedup = 8 / 3.5 ≈ 2.3x` ⚡
- Non-stop washing:
  - **Speedup =** `2n / (0.5n + 1.5) ≈ 4x` 🌀

> ✅ **Takeaway**: Pipelining = overlapping execution = major speedup 🔥

---

## 🧠 MIPS 5-Stage Pipeline 💡

1. **IF** – Instruction Fetch 🧾
2. **ID** – Instruction Decode & Register Read 🧠
3. **EX** – Execute or Address Calc 🔢
4. **MEM** – Access Memory 📦
5. **WB** – Write Back to Register ✍️

> 📦 Each instruction goes through **all 5 stages**, one per clock cycle

---

## ⏲️ **Pipeline vs. Single-Cycle Timing**

| Instruction | IF  | ID  | EX  | MEM | WB  | ⏱ Total (Single-Cycle) |
| ----------- | --- | --- | --- | --- | --- | ----------------------- |
| `lw`        | 200 | 100 | 200 | 200 | 100 | **800ps** 🐢            |
| `sw`        | 200 | 100 | 200 | 200 | —   | **700ps**               |
| `R-type`    | 200 | 100 | 200 | —   | 100 | **600ps**               |
| `beq`       | 200 | 100 | 200 | —   | —   | **500ps**               |

- ✅ **Pipelined Clock Time** = **200ps**
- ❌ **Single-Cycle Clock Time** = **800ps**

> 🔥 Speedup from pipelining = **ideal 4x** (if perfectly balanced)

---

## 🚀 Pipeline Speedup Magic

- 🧠 Speedup = `Time_nonpipelined / Time_pipelined`
- If all stages are equal → Speedup ≈ **# of stages**
- **BUT** real stages vary ➡️ actual speedup is less 🐌
- Pipelining boosts **throughput**, not individual instruction **latency**

---

## 🎯 MIPS: Pipelining-Friendly ISA 💖

MIPS is designed to pipeline smoothly like butter 🧈

1. ✅ All instructions = 32-bit ➡️ Easy decode 📏
2. ✅ Few formats ➡️ Quick decode + register read in 1 step 💨
3. ✅ Memory only used in `lw/sw` ➡️ Address in EX, Memory in MEM 📦
4. ✅ Word-aligned operands ➡️ No weird memory cases 🙅‍♀️

---

## ⚠️ Pipeline Hazards – The Enemies 👾

### 1️⃣ Structural Hazards 🛠️

- **Conflict for shared resources**
- E.g. One memory for both data and instructions ❌
- ❗ Solution: **Separate instruction/data memory** or **caches** 🧠

> Bubble = stall 🫧

---

### 2️⃣ Data Hazards 🔗

- When an instruction needs a result **before** it’s written 🔁

```assembly
add $s0, $t0, $t1
sub $t2, $s0, $t3  ← depends on result of add!
```

#### 🔄 Solution: **Forwarding / Bypassing**

- Use the result **as soon as it’s ready**, not when it’s written 😤
- Needs extra hardware to **grab data early** 🦾
- ⚠ Forward only forward in time… not back! (No time travel 😅)

---

### 3️⃣ Control Hazards 🎮

- Caused by **branches and jumps**
- Don’t know what to do until the branch decision is made 🤷
- Can lead to **bubbles (stalls)** if not handled smartly 🧠
- Solutions: branch prediction, delay slots, or better hazard handling 🌟

---

### ⛔ Load-Use Hazard – Can’t Always Forward

```assembly
lw $t1, 20($t0)
add $t2, $t1, $t3 ← needs $t1 value, but it’s not ready!
```

- ❌ You **can’t forward** data that **doesn’t exist yet** 😵‍💫
- Result: **Must insert a stall** 🚦
