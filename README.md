# 🖥️ 4-bit CPU Design — Computer Architecture Project

<div align="center">

**A fully functional 4-bit CPU designed and simulated using Logisim Evolution**

*Computer Architecture CS312/CSC323 — Dr. Khaled Elshafey — Spring 2025*

</div>

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [CPU Architecture](#-cpu-architecture)
- [Components](#-components)
- [Instruction Set](#-instruction-set)
- [Bonus Features](#-bonus-features)
- [How to Run](#-how-to-run)
- [Simulation Results](#-simulation-results)

---

## 🎯 Project Overview

This project presents the design and simulation of a simplified **4-bit Central Processing Unit (CPU)** built using **Logisim Evolution**. The CPU implements the fundamental components of a modern processor architecture:

- **ALU** — Performs arithmetic and logical operations
- **Register File** — Stores temporary values during computation
- **Control Unit** — Decodes instructions and generates control signals
- **Program Counter** — Tracks current instruction address
- **Memory (ROM)** — Stores program instructions

The CPU follows a standard **Fetch → Decode → Execute** cycle and supports 5 core instructions with 4 bonus features.

---


## 🏗️ CPU Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     4-bit CPU Datapath                       │
│                                                              │
│   ┌──────────┐    ┌──────────┐    ┌──────────────────────┐  │
│   │  Program │───▶│  Memory  │───▶│    Control Unit      │  │
│   │ Counter  │    │  (ROM)   │    │  (Instruction Decode)│  │
│   └──────────┘    └──────────┘    └──────────────────────┘  │
│        ▲                              │  ALU_OP              │
│        │                             │  REG_LOAD            │
│     Clock                            │  REG_SELECT          │
│                                      ▼                      │
│   ┌──────────┐    ┌──────────────────────────────────────┐  │
│   │ Register │◀───│              ALU                      │  │
│   │   File   │───▶│  ADD | SUB | AND | OR | XOR          │  │
│   │  (A, B)  │    │  Z_FLAG | C_FLAG | V_FLAG            │  │
│   └──────────┘    └──────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔧 Components

### ⚙️ ALU (Arithmetic Logic Unit) — Manar
The computational core of the CPU. Built with two subcircuits:
- **AU (Arithmetic Unit)** — Handles ADD and SUB using full adders
- **LU (Logic Unit)** — Handles AND, OR, XOR using logic gates
- A **MUX** selects the output based on the OP code

| Pin | Type | Width | Description |
|-----|------|-------|-------------|
| A | Input | 4-bit | First operand |
| B | Input | 4-bit | Second operand |
| OP | Input | 4-bit | Operation selector |
| Y | Output | 4-bit | Result |
| Z | Output | 1-bit | Zero flag |
| C | Output | 1-bit | Carry flag |
| V | Output | 1-bit | Overflow flag |

---

### 📦 Register File 
Two 4-bit registers built using **D flip-flops**:
- **Register A** — Stores first operand
- **Register B** — Stores second operand
- SELECT signal chooses which register to write
- Synchronized with the CPU clock

---

### 🧠 Control Unit 
Decodes 4-bit instructions into control signals:
- Uses a **decoder** to identify instruction type
- Generates: ALU_OP, REG_LOAD, REG_SELECT, MEM_WRITE
- Tested with all 5 supported instructions

---

### 🔢 Program Counter + Memory 
- **PC** auto-increments each clock cycle using an adder
- **RESET** returns PC to 0000
- **ROM (16×4)** stores up to 16 instructions
- PC_OUT connects to ROM address input

---

## 📟 Instruction Set

| Opcode | Instruction | ALU_OP | REG_LOAD | REG_SELECT | MEM_WRITE |
|--------|-------------|--------|----------|------------|-----------|
| `0000` | LOAD A | 000 | 1 | 0 | 0 |
| `0001` | LOAD B | 000 | 1 | 1 | 0 |
| `0010` | ADD | 000 | 0 | 0 | 0 |
| `0011` | SUB | 001 | 0 | 0 | 0 |
| `0100` | STORE | 000 | 0 | 0 | 1 |

### ALU Operation Codes

| Operation | OP Code | Example (A=1010, B=0101) | Result |
|-----------|---------|--------------------------|--------|
| ADD | `0000` | 1010 + 0101 | 1111 |
| SUB | `0001` | 1010 - 0101 | 0101 |
| AND | `0010` | 1010 AND 0101 | 0000 |
| OR | `0011` | 1010 OR 0101 | 1111 |
| XOR | `0100` | 1010 XOR 0101 | 1111 |

---

## ⭐ Bonus Features

### 1. Flag Register 
- **Zero Flag (Z)** → Set to 1 when ALU result = 0000
- **Carry Flag (C)** → Set to 1 when addition overflows
- Both flags visible as output pins in main_cpu
- Enables conditional operations

### 2. Jump Instruction — JZ 
- New instruction `0101` = Jump If Zero
- AND gate combines JZ detection + Z_FLAG
- JUMP_ENABLE output activates when Z=1 and instruction=0101
- Foundation of conditional branching and loops

| INSTRUCTION | Z_FLAG | JUMP_ENABLE | Action |
|-------------|--------|-------------|--------|
| 0101 (JZ) | 0 | 0 | Continue normally |
| 0101 (JZ) | 1 | 1 | Jump to new address |
| Other | Any | 0 | No jump |

### 3. 8-bit PC Upgrade 
- Extends Program Counter from **4-bit to 8-bit**
- Supports **256 instructions** instead of 16
- Wider register, adder, and ROM address bus
- File: `BonusFeatures/8bit_Upgrade/PC_8bit.circ`

---
## 🚀 How to Run

### Prerequisites
1. **Java** — Download from https://adoptium.net
2. **Logisim Evolution** — Download from https://github.com/logisim-evolution/logisim-evolution/releases

### Running the Main CPU
```bash
# Clone the repository
git clone https://github.com/Noor-Riyadh/cpu-4bit-project.git
cd cpu-4bit-project

# Open the main integrated CPU
# Launch Logisim Evolution, then:
# File → Open → ProgramCounter_Memory/PC_Memory.circ
# Click "main_cpu" in the left panel
# Switch to Simulate mode
# Click RESET to 0, then use the clock button to step through instructions
```

### Testing Individual Components
```
ALU:           File → Open → ALU/ALU.circut.circ
Register File: File → Open → Registers/Registers.circ
Control Unit:  File → Open → ControlUnit/ControlUnit.circ
PC + Memory:   File → Open → ProgramCounter_Memory/PC_Memory.circ
Jump (Bonus):  File → Open → BonusFeatures/JumpInstruction/Jump.circ
8-bit PC:      File → Open → BonusFeatures/8bit_Upgrade/PC_8bit.circ
```

```bash
# Switch to your branch
git checkout feature/ALU-manar        # Manar
git checkout feature/Registers-hala   # Hala
git checkout feature/ControlUnit-rawan # Rawan
git checkout feature/ProgramCounter-nada # Nada

# Pull latest changes before starting
git pull origin <your-branch>

# After working, push your changes
git add <your-folder>/
git commit -m "Description of what you did"
git push origin <your-branch>
```

---

## 📊 Simulation Results

### ALU Test Results
| Test | A | B | OP | Expected Y | Result |
|------|---|---|----|-----------|--------|
| ADD | 1010 | 0101 | 0000 | 1111 | ✅ Pass |
| SUB | 1010 | 0101 | 0001 | 0101 | ✅ Pass |
| AND | 1010 | 0101 | 0010 | 0000 | ✅ Pass |
| OR | 1010 | 0101 | 0011 | 1111 | ✅ Pass |
| XOR | 1010 | 0101 | 0100 | 1111 | ✅ Pass |

### Control Unit Test Results
| Test | INSTRUCTION | Expected Output | Result |
|------|-------------|----------------|--------|
| LOAD A | 0000 | REG_LOAD=1, REG_SELECT=0 | ✅ Pass |
| ADD | 0010 | ALU_OP=000 | ✅ Pass |
| STORE | 0100 | MEM_WRITE=1 | ✅ Pass |

### Program Counter Test Results
| Test | Action | Expected PC_OUT | Result |
|------|--------|----------------|--------|
| Reset | RESET=1 | 0000 | ✅ Pass |
| Clock 1 | Tick | 0001 | ✅ Pass |
| Clock 2 | Tick | 0010 | ✅ Pass |
| Clock 3 | Tick | 0011 | ✅ Pass |


<div align="center">

**Department of Computer Science | Spring 2025**

*Built with ❤️ by Team: Noor, Manar, Hala, Rawan, Nada*

</div>
