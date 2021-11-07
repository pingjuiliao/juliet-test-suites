## This branch test codes that are protected by shadow stack.
We are only interested in return address overwrite

## CWE121: Stack_Based_Buffer_Overflow
| Sink ID | status|reason/required operation if 'O' |
|--------|-------|----------|
| char_type_overrun_memcpy  |!| printLine() called with a overwritten buf ptr|
| char_type_overrun_memmove |!| printLine() called with a overwritten buf ptr|
| CWE129_connect_socket  |O| arbitrary write: 'nc -kl localhost 27015':26 | 
| CWE129_fgets           |O| arbitrary write: overwrite retaddr with :18  |
| CWE129_fscanf          |O| arbitrary write: overwrite retaddr with :14  | 
| CWE129_large           |!| arbitrary write but the offset is determined | 
| CWE129_listen_socket   |X| arbitrary write: 'nc localhost 27015': 26 | 
| CWE129_rand            |!| arbitrary write with random offset | 
| CWE131_loop            |!| infinite loop due to overwritten data |
| CWE131_memcpy          |C| alloc() allocates enough size | 
| CWE131_memmove         |C| alloc() allocates enough size |
| CWE135                 |!| printLine() called with a overwritten buf ptr|
| CWE193_char_alloca_cpy |X| one-byte off overwrite |

- O: shadow stack correctly protects return address 
- !: needs source code modification to handle it
- C: compiler issue: it's now impossible to overwrite retaddr due to compiler
- X: conceptually impossible to overwrite return addresses 

