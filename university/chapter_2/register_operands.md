# Register Operands

---

Arithmetics instructions use register operands

# MIPS

- MIPS has a 32\*32-bit register file
- Numbered 0 to 31, ex: $0 - $31
- 32-bit data called a "word" in MIPS architecture

# Design Principle 2: Smaller is faster

- A very large number of registers may increase the clock cycle time
- Using more than 32 registers may take more bits in the instruction format

# Assembler names

```
$s0, $s1, ..., $s7 for saved variables. Ex: $t0 = g + h
$t0, $t1, ..., $t9 for temporary values. Ex: $t1 = i + j
```
