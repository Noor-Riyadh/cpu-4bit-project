# Control Unit Design

## Description
The Control Unit acts as the central processor's brain. It decodes 4-bit instructions 
to generate signals that control the ALU, Registers, and Memory.

## Truth Table
This table shows how each instruction (Input) affects the control signals (Outputs):

| Instruction | Binary | REG_SELECT | REG_LOAD | MEM_WRITE | ALU_OP |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **LOAD A** | 0000 | 0 | 1 | 0 | 000 |
| **LOAD B** | 0001 | 1 | 1 | 0 | 000 |
| **ADD** | 0010 | X | 0 | 0 | 000 |
| **SUB** | 0011 | X | 0 | 0 | 001 |
| **STORE** | 0100 | X | 0 | 1 | 000 |
|**JZ** |0101 |X |0 |0 |000 |1*

## Implementation Details
- **Decoder:** A 4-to-16 line decoder is used to isolate each specific instruction.
- **Logic Gates:** An OR gate is used for `REG_LOAD` so it activates for both LOAD A and LOAD B.
- **ALU Control:** A splitter is used to map specific decoder outputs to the 3-bit `ALU_OP` bus.