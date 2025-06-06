# Week 13 assignment

---

4.13 This exercise is intended to help you understand the relationship between
forwarding, hazard detection, and ISA design. Problems in this exercise refer to the
following sequence of instructions, and assume that it is executed on a 5-stage
pipelined datapath:

```assembly
add r5,r2,r1
lw r3,4(r5)
lw r2,0(r2)
or r3,r5,r3
sw r3,0(r5)
```

4.13 If there is forwarding, for the first five cycles during the execution of this code,
specify which signals are asserted in each cycle by hazard detection and forwarding
units in Figure 4.60.

---

## 4.13

| Cycle | EX  | PC write | ALUin 1 | ALUin 2 |
| ----- | --- | -------- | ------- | ------- |
| 1     | -   | 1        | x       | x       |
| 2     | -   | 1        | x       | x       |
| 3     | l1  | 1        | 0       | 0       |
| 4     | l2  | 1        | 1       | 0       |
| 5     | l3  | 1        | 0       | 0       |

PCWrite = 1: No Load-Use hazard, no stall

ALUin1/ALUin2:
• 0 = From Register File
• 1 = Forward from EX/MEM stage
• X = Don't care (ALU not used yet)
