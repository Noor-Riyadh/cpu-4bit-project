"# ALU Truth Table - Manar"

cat > ALU/ALU\_truth\_table.md << 'EOF'

\# ALU Truth Table — Manar



\## OP Code Reference

| Operation | OP Code |

|-----------|---------|

| ADD       | 0000    |

| SUB       | 0001    |

| AND       | 0010    |

| OR        | 0011    |

| XOR       | 0100    |



\## Test Results

| A    | B    | OP   | Y    | Result |

|------|------|------|------|--------|

| 1010 | 0101 | 0000 | 1111 | ADD  |

| 1010 | 0101 | 0001 | 0101 | SUB  |

| 1010 | 0101 | 0010 | 0000 | AND  |

| 1010 | 0101 | 0011 | 1111 | OR   |

| 1010 | 0101 | 0100 | 1111 | XOR  |

EOF

