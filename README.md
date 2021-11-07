## This branch tests shadow stack that guard return address only:
Therefore, we only interested in the bugs that overwrite the return addresses/


## CWE121: Stack_Based_Buffer_Overflow
| Bug ID | Interested: Reason |
|--------|--------------------|
| CWE129_rand_*    | !: arbitrary write with arbitrary index | 
| CWE131_loop_*    | !: infinite loop |
| CWE131_memcpy_*  | !: compiler reserves enough space (!: 73.cpp)|
| CWE131_memmove_* | !: compiler reserves enough space (!: 73.cpp)|
| CWE135_*                  | !: cpp |
| CWE193_char_alloca_cpy_* | X: One-byte overflow | 

O: Overwritten return addresses detected!
X: conceptually impossible to overwrite return addresses
!: needs source code modification to overwrite return addresses


## CWE562
It's

## CWE252 & CWE253
It's for return value, not return address
