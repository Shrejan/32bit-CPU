# 📘 CPU Architecture & Instruction Set Documentation

This document describes the **CPU architecture** and the **instruction set design** implemented in this processor.

The CPU supports three instruction types:
- R-Type (Register Instructions)
- I-Type (Immediate / Memory / Branch / I-O)
- J-Type (Jump Instructions)

---

# 🧠 CPU Architecture

## Core Components

The processor consists of the following modules:

- Program Counter (PC)
- Instruction Memory
- Control Unit
- Register File
- ALU (Arithmetic Logic Unit)
- Data Memory
- Memory Mapped I/O
- Instruction Decoder

---

## Instruction Execution Cycle

1. Fetch instruction from Instruction Memory using PC
2. Decode instruction
3. Read registers
4. Execute operation
5. Access memory (if required)
6. Write result back
7. Update PC

---

# 🧩 Instruction Formats

---

# 1️⃣ R-Type Instructions

Used for register-to-register operations.

## Format

| OPCODE | FUNCT | RD | RT | RS | SHAMT |
|-------|--------|----|----|----|-------|
| 6 bit | 6 bit  | 5  | 5  | 5  |   5   |

## Field Description

| Field | Description |
|------|-------------|
| OPCODE | Instruction type |
| RS | Source Register 1 |
| RT | Source Register 2 |
| RD | Destination Register |
| SHAMT | Shift Amount |
| FUNCT | Operation selector |

## Supported Instructions

| Instruction | Operation | Description |
|------------|-----------|-------------|
| ADD | RD = RS + RT | Addition |
| SUB | RD = RS - RT | Subtraction |
| AND | RD = RS & RT | Bitwise AND |
| OR | RD = RS \| RT | Bitwise OR |
| XOR | RD = RS ^ RT | XOR |
| SLT | RD = (RS < RT) | Set if less than |
| SLL | RD = RT << SHAMT | Shift Left |
| SRL | RD = RT >> SHAMT | Shift Right |

---

# 2️⃣ I-Type Instructions

Used for memory access, branching, immediate operations, and I/O.

## Format

| OPCODE | RS | RT | IMMEDIATE |
|-------|----|----|-----------|
| 6 bit | 5  | 5  | 16 bit    |

## Field Description

| Field | Description |
|------|-------------|
| OPCODE | Instruction type |
| RS | Base Register |
| RT | Target Register |
| IMMEDIATE | Constant / Address Offset |

---

## Load & Store Instructions

| Instruction | Operation | Description |
|------------|-----------|-------------|
| LOAD | RT = MEM[RS + IMM] | Load from memory |
| STORE | MEM[RS + IMM] = RT | Store to memory |

---

## Branch Instructions

### Basic Branch

| Instruction | Condition |
|------------|-----------|
| BEQ | Branch if RS == RT |
| BNE | Branch if RS != RT |

### Conditional Branch

| Instruction | Condition |
|------------|-----------|
| BGT | Branch if RS > RT |
| BLT | Branch if RS < RT |

---

# ⌨️ Memory Mapped I/O

This CPU uses memory-mapped addresses for keyboard input and ASCII display.

## Keyboard Input

Instruction:
IN RT

Operation:
RT = Keyboard ASCII Value

Description:
Reads input from keyboard and stores ASCII value in register.

---

## ASCII Display Output

Instruction:
OUT RT

Operation:
Display ASCII(RT)

Description:
Displays ASCII character stored in register.

---

# 3️⃣ J-Type Instructions

Used for program control flow.

## Format

| OPCODE | ADDRESS |
|-------|---------|
| 6 bit | 26 bit  |

## Supported Instructions

| Instruction | Operation | Description |
|------------|-----------|-------------|
| JMP | PC = ADDRESS | Jump to address |
| CALL | Save PC and Jump | Function call |
| RET | Return to saved PC | Return from function |

---

# 🗂 Register File

Example register layout:

| Register | Name | Description |
|---------|------|-------------|
| R0 | ZERO | Constant zero |
| R1 | TEMP1 | Temporary register |
| R2 | TEMP2 | Temporary register |
| R3 | TEMP3 | Temporary register |
| R4 | INPUT | Keyboard input |
| R5 | OUTPUT | ASCII display |

(Modify according to your design)

---

# 🧭 Memory Map

Address Range | Purpose
--------------|---------
0x0000 – 0x0FFF | Instruction Memory
0x1000 – 0x1FFF | Data Memory
0x2000 | Keyboard Input
0x2004 | ASCII Display

---

# 🧪 Example Program

Keyboard Input → Store → Load → Display

```
IN R1
STORE R1, 0(R0)
LOAD R2, 0(R0)
OUT R2
```

Execution Flow:

User presses key  
→ Keyboard sends ASCII  
→ Stored in Register  
→ Stored in Memory  
→ Loaded again  
→ Displayed on ASCII display

---

# 🧾 Instruction Encoding Summary

R-Type → Register operations  
I-Type → Immediate / Memory / Branch / I-O  
J-Type → Jump instructions

---

# 🚀 Future Improvements

Possible upgrades for this CPU:

- Pipeline implementation
- Interrupt support
- Cache memory
- Extended instruction set
- Faster execution
