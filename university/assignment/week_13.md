# 🌟 Week 13: Forwarding & Hazard Detection in a Pipelined Wonderland\~ 🛠️✨

## 🧩 Topic: Forwarding, Hazard Detection, and ISA Design

We're diving into the enchanted world of pipelined datapaths! 🌈✨
This exercise explores how forwarding and hazard detection mechanisms help MIPS instructions flow smoothly through the pipeline like a melody\~ 🎵

---

## 📜 Instruction Spell Sequence ✨

```assembly
add r5, r2, r1     ; ➕ Calculate r5 = r2 + r1
lw  r3, 4(r5)      ; 📦 Load value from memory into r3 using r5 as base
lw  r2, 0(r2)      ; 📦 Load value into r2 from memory
or  r3, r5, r3     ; 🔁 Bitwise OR of r5 and r3 -> r3
sw  r3, 0(r5)      ; 📤 Store r3 into memory at address in r5
```

---

## 🔍 4.13 Analysis: Cycle-by-Cycle Hazard & Forwarding Signal Flow 🔄✨

We’re focusing on the **first 5 cycles**—the most magical part where forwarding decisions shape the path of destiny! 💫

> Let’s see what happens to each signal! 😮✨

| ⏱️ Cycle | ✨ EX Hazard Level | 🚦 PCWrite | ⚡ ALUin1 | ⚡ ALUin2 |
| -------: | -----------------: | ---------: | --------: | --------: |
|        1 |      - (no hazard) |       ✔️ 1 |      ❓ x |      ❓ x |
|        2 |      - (no hazard) |       ✔️ 1 |      ❓ x |      ❓ x |
|        3 |   🟠 `l1` Detected |       ✔️ 1 |      🟥 0 |      🟥 0 |
|        4 |   🟡 `l2` Detected |       ✔️ 1 |      ✅ 1 |      🟥 0 |
|        5 |   🔵 `l3` Detected |       ✔️ 1 |      🟥 0 |      🟥 0 |

🧠 **Signal Meanings:**

- **PCWrite = 1** ✔️ → No stall needed! The processor happily continues fetching the next instruction\~ 🏃‍♀️✨
- **ALUin1 / ALUin2:**

  - `0` = Value from Register File 🧾
  - `1` = Forwarded from EX/MEM 📨
  - `x` = Don’t care (ALU isn’t even doing magic yet 💭)

---

## 🪄 Storytime Summary 🌸

🔧 _What’s happening in each cycle? Let’s break it down\~_

1️⃣ **Cycle 1:**

- `add` begins its journey through IF 💖 No hazards yet, everyone's just warming up.

2️⃣ **Cycle 2:**

- `lw` starts, still no hazard—our party is gathering their gear 🏕️

3️⃣ **Cycle 3:**

- First true hazard! `lw` needs the result of `add`, but forwarding isn't ready yet! So... we mark it as **l1** and use the register value anyway 🟥

4️⃣ **Cycle 4:**

- `lw r2, 0(r2)` enters, but our `or` instruction now gets data _magically forwarded_ from `EX/MEM`—✨yay forwarding!✨

5️⃣ **Cycle 5:**

- `sw` gets ready to store the magic, needing inputs just like `or`, so forwarding continues to keep the spell alive\~

---

## 🧁 TL;DR — Sparkle Recap 🌟

✔️ **Forwarding** helps avoid stalling by passing results directly between pipeline stages like a helpful fairy\~ 🧚
✔️ **Hazard Detection Unit** watches closely for risky moments when data dependencies might break the flow\~
✔️ In this 5-cycle journey, thanks to forwarding, **no stalls were needed** 💪✨

> 📌 Forwarding isn’t just helpful… it's **essential** for efficient pipelined execution! Like teamwork in a magical guild\~ 🌟🛡️
