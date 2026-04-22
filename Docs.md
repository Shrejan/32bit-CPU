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
| FUNCT | Operation selector |
| RD | Destination Register |
| RT | Source Register 1 |
| RS | Source Register 2 |
| SHAMT | Shift Amount |


## Supported Instructions

| Instruction | Operation | Description |
|------------|-----------|-------------|
| ADD | RD = RS + RT | Addition |
| SUB | RD = RS - RT | Subtraction |
| AND | RD = RS & RT | Bitwise AND |
| OR | RD = RS \| RT | Bitwise OR |
| SLT | RD = (RS < RT) | Set if less than |
| SLL | RD = RT << SHAMT | Shift Left |
| SRL | RD = RT >> SHAMT | Shift Right |

---

# 2️⃣ I-Type Instructions

Used for memory access, branching, immediate operations, and I/O.

## Format

| OPCODE | RT | RS | IMMEDIATE |
|-------|----|----|-----------|
| 6 bit | 5  | 5  | 16 bit    |

## Field Description

| Field | Description |
|------|-------------|
| OPCODE | Instruction type |
| RT | Target Register |
| RS | Base Register |
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


# 🧭 Memory Map

Address Range | Purpose
--------------|---------
 0xFFFFF1 | Data Flag
 0xFFFFF0 | Keyboard Input
 0xFFFFF2| ASCII Display
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
| R4 | TEMP3 | Temporary register |
| R5 | TEMP3 | Temporary register |
| R6 | INPUT | Keyboard input |
| R7 | OUTPUT | ASCII display |

(Modify according to your design)

# 🔍 Instruction Decode of Example Program

This section explains how each machine instruction is decoded by the CPU.
The instruction is divided into fields according to the CPU instruction format.

Example Program

```
00000000
20250000
0C220000
20260000
24270000
28000000
```

---

# Instruction 1

Machine Code
```
00000000
```

Binary Representation
```
000000 00000 00000 00000 00000 000000
```

Decoded Fields

| Field | Value | Description |
|------|------|-------------|
| Opcode | 000000 | NOP / Start Instruction |
| RS | 00000 | Register 0 |
| RT | 00000 | Register 0 |
| RD | 00000 | Register 0 |
| SHAMT | 00000 | No shift |
| FUNCT | 000000 | No operation |

Purpose:
Start execution from address 0.

---

# Instruction 2

Machine Code
```
20250000
```

Binary Representation
```
001000 00001 00101 0000000000000000
```

Decoded Fields

| Field | Value | Description |
|------|------|-------------|
| Opcode | 001000 | LOAD Instruction |
| RS | 00001 | Source Register |
| RT | 00101 | Destination Register |
| Immediate | 0000 | Offset |

Operation

```
R1 ← MEM[R5]
```

Description

Continuously loads the keyboard status value from the memory-mapped address
stored in **Register 5 (FFFFF1)**.

---

# Instruction 3

Machine Code
```
0C220000
```

Binary Representation
```
000011 00001 00010 0000000000000000
```

Decoded Fields

| Field | Value | Description |
|------|------|-------------|
| Opcode | 000011 | Branch Instruction |
| RS | 00001 | Register 1 |
| RT | 00010 | Register 2 |
| Immediate | 0000 | Branch Target |

Operation

```
IF (R1 == R2) CONTINUE
ELSE JUMP TO 00000000
//where R2=00001
```

Description

Checks whether a key has been pressed.

---

# Instruction 4

Machine Code
```
20260000
```

Binary Representation
```
001000 00001 00110 0000000000000000
```

Decoded Fields

| Field | Value | Description |
|------|------|-------------|
| Opcode | 001000 | LOAD |
| RS | 00001 | Base Register |
| RT | 00110 | Target Register |
| Immediate | 0000 | Offset |

Operation

```
R6 ← MEM[FFFFF0]
```

Description

Loads ASCII value of the pressed key.

---

# Instruction 5

Machine Code
```
24270000
```

Binary Representation
```
001001 00001 00111 0000000000000000
```

Decoded Fields

| Field | Value | Description |
|------|------|-------------|
| Opcode | 001001 | STORE |
| RS | 00001 | Source Register |
| RT | 00111 | Address Register |
| Immediate | 0000 | Offset |

Operation

```
MEM[FFFFF2] ← ASCII VALUE
```

Description

Writes the ASCII value to the display.

---

# Instruction 6

Machine Code
```
28000000
```

Binary Representation
```
001010 00000000000000000000000000
```

Decoded Fields

| Field | Value | Description |
|------|------|-------------|
| Opcode | 001010 | JUMP |
| Address | 00000000 | Jump Target |

Operation

```
PC ← 00000000
```

Description

Creates an infinite loop.

---

# Complete Program Flow

```
Start Execution
      ↓
Check Keyboard Status
      ↓
Is Key Pressed?
      ├── No → Jump to Start
      │
      └── Yes
            ↓
      Read ASCII Value
            ↓
      Send to Display
            ↓
      Jump to Start
```

---

# What This Program Demonstrates

This example shows how the CPU handles:

• Memory-Mapped I/O  
• Polling for input  
• Branching logic  
• Jump instructions  
• Infinite loop execution

# 🚀 Future Improvements

Possible upgrades for this CPU:

- Pipeline implementation
- Interrupt support
- Cache memory
- Extended instruction set
- Faster execution
