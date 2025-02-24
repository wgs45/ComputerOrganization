# Arithmetics operations

---

# Add and subtract, three operands

- Two sources and one destination

```
add a, b, c  # a gets b + c

Operator, Operands (variables), Comments using #
```

Each line can contain at most one instruction
Comments always terminate at the end of a line

- All arithmetics operations have exactly three operands, no more and no less
  <br>

# Design Principle 1: Simplicity favors regularity

- Regularity makes implementation simpler
- Simplicity enables higher performance at lower cost

# Arithmetic Example

- C Code:

```
f = (g + h) - (i + j)
```

- Compiled MIPS code:

```
add t0, g, h # temp t0 = g + h
add t1, i, j # temp t1 = i + j
sub f, t0, t1 # f = t0 - t1
```
