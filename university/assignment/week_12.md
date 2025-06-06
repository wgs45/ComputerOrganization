# 🌟 Week 12 – Pipeline Hazards & Performance ✨

_“A graceful dance through the stages of MIPS... but beware of hazards lurking between the lines\~!”_ 💃🧙‍♀️

---

## 🧩 4.10.1 – **One Memory = One Problem?!** 😱💾

> “What happens when code & data fight over the same memory crystal?” 💥📖🔮

### 🔹 🧠 **Key Assumptions:**

- ✅ **Perfect Branch Prediction** (no control hazards 💃)
- ❌ **No delay slots**
- 💥 **Only ONE memory** for both **instructions + data** ❗
- 📚 **Data access wins** the conflict (because we _need_ our precious values\~)

---

### 🔸 MIPS Code Breakdown

```assembly
sw r16, 12(r6)     # Store → MEM access ❗
lw r16, 8(r6)      # Load  → MEM access ❗
beq r5, r4, Label  # Branch (but perfectly predicted 🧠✨)
add r5, r1, r4     # Just ALU
slt r5, r15, r4    # Another ALU op
```

### 🧮 Let’s Calculate\~! 💫

1. **Ideal Pipeline Execution (No Hazards):**
   ➤ 5 instructions need: `5 + 5 - 1 = 9 cycles` ⏳

2. **Structural Hazards Detected:**

   - 🧱 `sw` + next `lw` → conflict! (MEM vs IF)
   - 🧱 `lw` + next `beq` → another conflict!
     ✨ **= 2 total stalls** 🛑🛑

3. **Adjusted Total Cycles:**
   ✔️ `9 + 2 = 11 cycles`

4. **Clock Cycle Time:**
   🔧 Max latency stage = **IF = 200ps**

5. **Final Execution Time:**
   🕒 `11 × 200ps = 2200ps` 💥

---

### ❓ Can we fix it with NOPs?

> “Just sprinkle in a few NOPs... right? 😅”

**Nope! 🚫**
Even if we insert NOPs, _they still need to be fetched!_ Which means...
→ ❗ Instruction memory is still blocked during MEM access
→ NOPs don't solve this kind of hazard 😢

💡 **Real fix?** Use **separate instruction + data memory** (aka **Harvard architecture**!) 🧙‍♀️✨

---

### 💖 TL;DR

- ✨ Total Time: **2200ps**
- 🔥 Stalls from MEM/IF conflicts = **2**
- 🛠️ NOPs won’t help here 💔
- 💡 Use split memory to avoid this forever\~

---

## 🚩 4.10.3 – **Branch Stalls: ID vs EX Decision** 🎯

_“Should we peek into the future early, or wait a bit longer?”_ 🔮

---

### 🔸 Concepts

- **Stall-on-branch**: Don't fetch next instr. until the branch is resolved ❗
- **No delay slots** (like stepping carefully so we don’t trip\~)
- 🔍 Compare decision point:

  - EX stage → ⏱️ resolved _late_
  - ID stage → 🧠 resolved _early_

---

### 🔢 Calculation Time! 🧙‍♀️

| Case           | Total Cycles          |
| -------------- | --------------------- |
| 🧠 ID decision | 9 + 1 = **10** cycles |
| ⏱️ EX decision | 9 + 2 = **11** cycles |

### 🚀 Speedup

> `Speedup = Old / New = 11 / 10 = **1.10x**` 🎉✨

---

### 💖 TL;DR

- ⛔ EX stage causes a **2-cycle** delay
- 🧠 ID stage only delays **1 cycle**
- ⭐ **Speedup = 1.10x** = smoother execution\~!

---

## 🔧 4.10.5 – **Latency Shift & Speed Magic** ✨⏱️

_“What if we trained our ID stage to think faster... or at least think \_earlier_?”\_ 💡

---

### 🧠 Changes When Moving Branch Decision

- 🔼 ID latency increases by 50%: `120 → 180 ps`
- 🔽 EX latency decreases by 10ps: `150 → 140 ps`

---

### 🛠️ Pipeline Clock (still ruled by slowest stage)

| Stage    | EX Decision | ID Decision |
| -------- | ----------- | ----------- |
| IF       | 200 ps      | 200 ps      |
| ID       | 120 ps      | **180 ps**  |
| EX       | 150 ps      | **140 ps**  |
| MEM      | 190 ps      | 190 ps      |
| WB       | 100 ps      | 100 ps      |
| 🔔 Clock | **200 ps**  | **200 ps**  |

💡 Max stage remains **200ps** (no change)

---

### ⏱️ Total Time Comparison

| Decision Point | Cycles | Total Time          |
| -------------- | ------ | ------------------- |
| EX             | 11     | 11×200 = **2200ps** |
| ID             | 10     | 10×200 = **2000ps** |

✨ **Speedup = 2200 / 2000 = 1.10x** again\~!

---

### 💖 TL;DR

- Clock doesn’t change (still ruled by IF = 200ps)
- ID shift saves 1 cycle despite ID getting slower
- ⭐ Still achieves a sweet **1.10x speedup**\~!
