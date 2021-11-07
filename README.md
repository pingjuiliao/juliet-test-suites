## This branch test codes that are protected by shadow stack.
We are only interested in return address overwrite

## CWE121: Stack_Based_Buffer_Overflow
| CWE ID | status/reason |
|--------|---------------|
| CWE129_listen_socket_* | 
| CWE129_rand_* | !: arbitrary write with random offset 

- O: shadow stack correctly protects 
- !: needs source code modification to handle it
- X: conceptually impossible to overwrite return addresses 

