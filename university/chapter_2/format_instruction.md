# MIPS Instructions

---

# MIPS R-format instructions

| op     | rs     | rt     | rd    | shamt  | fucnt  |
| ------ | ------ | ------ | ----- | ------ | ------ |
| 6 bits | 5 bits | 5 bits | 5bits | 5 bits | 6 bits |

## Instruction fields

- op: operation code (opcode)
- rs: first register source operand
- rt: second register source operand
- rd: register destination operand
- shamt: shift amount
- funct: function code (extends opcode)

# MIPS I-format instructions

| op     | rs     | rt     | constant or address |
| ------ | ------ | ------ | ------------------- |
| 6 bits | 5 bits | 5 bits | 16 bits             |

## Immediate arithmetic and load/store instructions

- rt: destination register number for lw, or source register number for sw
- Constant: -2^15 to +2^15 - 1
- Address: offset added to base address in rs

## Design principle 4: Good design demands good compromises

- Different formats complicate decoding, but allow 32-bit instructions uniformly
- Keeps formats as similar as possible

## Examples
