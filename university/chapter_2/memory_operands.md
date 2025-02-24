# Memory Operands

---

# Main Memory

- Main memory used for composite data. Ex: Arrays, structures (More complex data structures)
- Arithmetic operations occur only on registers.
- MIPS must include "data transfer instructions" to transfer data between memory and registers

# Memory

- A large, single dimensional array. With address called index, starting at 0
- Ex: address of 3rd data element is 2, and value of Memory[2] is 10
- Memory is byte address, each address identifies an 8-bit byte
- Words are aligned in memory, address must be a multiple of 4 (Alignment Restrictions)

# Apply Arithmetic Operations

- Load values from memory into registers (lw = load word)
- Store result from register to memory (sw = store word)

# MIPS

- MIPS is Big Endian
- Most-significant byte at least address of a word
- Little Endian: least-significant byte at least address

# Memory Operand Example 1

- C code:

```
g = h + A[8];
```

(g in $s1, h in $s2, base address of A in $s3)

- Compiled MIPS Code:

```
lw $t0, 32($s3) # load word
add $s1, $s2, $t0
```

(32 is an offset, ($s3) is an base register)

# Memory Operand Example 2

- C code:

```
A[12] = h + A[8];
```

(h in $s2, base address of A in $s3)

- Compiled MIPS Code:

```
lw $t0, 32($s3) # load word
add $t0, $s2, $t0
sw $t0, 48($s3) # store word
```

(Index 8 requires offset of 32 and index 12 requires offset of 48)
