Nada - Program Counter and Memory



Design Description



The Program Counter is built using a 4-bit Register and a 4-bit Adder to increment (+1) automatically.

It has a Clock input to count and a Reset input to go back to zero.

I used a 16×4 ROM to store the instructions.



Stored Instructions in ROM:



| Address | Instruction | Meaning   |

|---------|-------------|-----------|

| 0000    | 0000        | LOAD A    |

| 0001    | 0001        | LOAD B    |

| 0010    | 0010        | ADD       |

| 0011    | 0011        | SUB       |

| 0100    | 0100        | STORE     |



Testing Results



Reset works: PC returns to 0000.

Clock works: PC increments correctly (0000 → 0001 → 0010 → 0011 → 0100...).

INSTRUCTION\_OUT shows the correct instruction for each address.

