# 🖥️ 32-Bit CPU Architecture in Logisim

![Project Banner](images/32bit_computer.png)

A **fully modular 32-bit CPU design** built using **Logisim**, demonstrating how a processor works internally using fundamental computer architecture components such as:

* Program Counter
* Register File
* Control Unit
* Memory-Mapped I/O
* ALU
* Instruction Flow System

This project is designed for **students, beginners, and hardware enthusiasts** who want to explore CPU design at the circuit level.

---

# 🚀 Project Highlights

✔ 32-bit CPU architecture
✔ Modular block-based design
✔ Educational CPU implementation
✔ Memory-mapped I/O support
✔ Custom instruction execution flow
✔ Easy to understand circuit layout
✔ Ready to simulate in Logisim

---

# 📸 CPU Architecture Overview

## Full CPU Circuit

![CPU Architecture](images/cpu.png)

---

# 🧠 Main Components

## Program Counter

Tracks the address of the next instruction.

![Program Counter](images/program_counter.png)

---

## Register Block

Stores intermediate data during instruction execution.

![Registers](images/register.png)

---

## Control Unit

Controls instruction execution and generates control signals.

![Control Unit](images/controll_unit.png)

---

## Memory Mapped I/O

Allows interaction with external input/output using memory addresses.

![Memory Mapped IO](images/memo_io.png)

---

## ALU (Arithmetic Logic Unit)

Performs arithmetic and logical operations.

![ALU](images/ALU.png)

---

# 🏗️ Project Structure

```
32-bit-cpu-logisim/
│
├── cpu.circ
├── README.md
│
├── images/
│   ├── full-cpu.png
│   ├── program-counter.png
│   ├── register-block.png
│   ├── control-unit.png
│   ├── memory-io.png
│   └── alu.png
│
└── docs/
    └── instruction-set.md
```

---

# 📦 Requirements

To run this project you need:

* Logisim or Logisim Evolution
* Basic knowledge of CPU architecture (optional but helpful)

---

# ▶️ How to Run the CPU Simulation

Step 1
Download or clone the repository.

Step 2
Open **Logisim**.

Step 3
Open the main circuit file:

```
cpu.circ
```

Step 4
Start the simulation clock.

Step 5
Observe how instructions move through the CPU.

---

# 📥 How to Clone / Pull This Project

Anyone can download and run this project using Git.

### Clone the repository

```
git clone https://github.com/Shrejan/32bit-CPU.git
```

### Move into the project folder

Then open:

```
cpu.circ
```

in Logisim.

---

# 🌍 Alternative Download Method

If you don't use Git:

1 Open the repository page
2 Click **Code**
3 Click **Download ZIP**
4 Extract the project
5 Open `cpu.circ` in Logisim

---

# ⚙️ Instruction Cycle (How the CPU Works)

The CPU executes instructions in the following stages:

1 Fetch
Program Counter selects the next instruction.

2 Decode
Control Unit interprets the instruction.

3 Execute
ALU performs operations.

4 Memory Access
Reads or writes data.

5 Write Back
Result stored into registers or output.

---

# 📊 Future Improvements

Planned upgrades for the CPU:

* Custom instruction set expansion
* Branching and jump improvements
* Advanced ALU operations
* Cache memory simulation
* Instruction visualizer
* Debug mode for CPU

---

# 📚 Educational Purpose

This project helps understand:

* CPU design
* Instruction execution
* Digital logic architecture
* Processor pipelines (basic concept)
* Hardware level computing

---

# 👨‍💻 Author

**Shrejan Kotyan**

Creator of this 32-bit CPU project.

Focused on:

* Computer Architecture
* AI Systems
* Hardware + Software Integration

---

# ⭐ Support the Project

If you like this project:

⭐ Star the repository
🛠 Improve the design
📢 Share with others

---

# 📜 License

This project is released for **educational use**.

---

# 📷 More Screenshots Coming Soon

Additional circuit diagrams will be uploaded:

* Data Path
* Instruction Decoder
* Clock System
* Memory Interface
* Execution Flow
