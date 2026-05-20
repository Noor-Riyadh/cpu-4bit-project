# 4-bit CPU Design — Logisim Evolution

A fully functional 4-bit CPU designed and simulated using Logisim Evolution as part of a Computer Architecture course project.

---

## CPU Architecture

```
Program Counter → Memory → Control Unit → ALU → Register File
                                ↑                      ↓
                             Clock              Result stored back
```

---

## Components

| Component | File | Description |
|-----------|------|-------------|
| ALU | `ALU/ALU.circut.circ` | ADD, SUB, AND, OR, XOR operations |
| Register File | `Registers/Registers.circ` | Two 4-bit registers using D flip-flops |
| Control Unit | `ControlUnit/ControlUnit.circ` | 4-bit instruction decoder |
| PC + Memory | `ProgramCounter_Memory/PC_Memory.circ` | Auto-incrementing PC + ROM |
| Main CPU | `ProgramCounter_Memory/PC_Memory.circ → main_cpu` | Full integrated circuit |

---

## Instruction Set

| Opcode | Instruction | ALU_OP | REG_LOAD | REG_SELECT | MEM_WRITE |
|--------|-------------|--------|----------|------------|-----------|
| `0000` | LOAD A | 000 | 1 | 0 | 0 |
| `0001` | LOAD B | 000 | 1 | 1 | 0 |
| `0010` | ADD | 000 | 0 | 0 | 0 |
| `0011` | SUB | 001 | 0 | 0 | 0 |
| `0100` | STORE | 000 | 0 | 0 | 1 |

---

## ALU Operations

| OP Code | Operation | A=1010, B=0101 | Result |
|---------|-----------|----------------|--------|
| `0000` | ADD | 1010 + 0101 | 1111 |
| `0001` | SUB | 1010 - 0101 | 0101 |
| `0010` | AND | 1010 AND 0101 | 0000 |
| `0011` | OR | 1010 OR 0101 | 1111 |
| `0100` | XOR | 1010 XOR 0101 | 1111 |

---

## Bonus Features

| Feature | File | Description |
|---------|------|-------------|
| Flag Register | `ALU/ALU.circut.circ` | Zero (Z) and Carry (C) flags |
| Jump Instruction (JZ) | `BonusFeatures/JumpInstruction/Jump.circ` | Conditional branch when Z=1 |
| 8-bit PC Upgrade | `BonusFeatures/8bit_Upgrade/PC_8bit.circ` | Extends PC to support 256 instructions |

---

## How to Run

**Requirements:** Java + Logisim Evolution (`logisim-evolution-*.jar`)

```bash
# Run Logisim
java -jar logisim-evolution-*.jar

# Then: File → Open → select the .circ file you want to test
```

**To run the full integrated CPU:**
1. Open `ProgramCounter_Memory/PC_Memory.circ`
2. Click `main_cpu` in the left panel
3. Switch to **Simulate** mode
4. Set RESET = 0
5. Click the clock button to step through instructions

---

## Tools Used

- [Logisim Evolution v4.1.0](https://github.com/logisim-evolution/logisim-evolution)
- Git + GitHub for version control
