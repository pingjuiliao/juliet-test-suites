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
| CWE129_listen_socket   |O| arbitrary write: 'nc localhost 27015': 26 | 
| CWE129_rand            |!| arbitrary write with random offset | 
| CWE131_loop            |!| infinite loop due to overwritten data |
| CWE131_memcpy          |C| alloc() allocates enough size | 
| CWE131_memmove         |C| alloc() allocates enough size |
| CWE135                 |!| printLine() called with a overwritten buf ptr|
| CWE193_char_alloca_cpy     |C| one-byte off overflow/ enough stack space | 
| CWE193_char_alloca_loop    |C| one-byte off overflow/ enough stack space |
| CWE193_char_alloca_memcpy  |C| one-byte off overflow/ enough stack space | 
| CWE193_char_alloca_memmove |C| one-byte off overflow/ enough stack space |
| CWE193_char_alloca_ncpy    |C| one-byte off overflow/ enough stack space |
| CWE193_char_declare_cpy    |!| one-byte off overflow |
| CWE193_char_declare_loop   |!| one-byte off overflow |
| CWE193_char_declare_memcpy |!| one-byte off overflow | 
| CWE193_char_declare_memmove|!| one-byte off overflow |
| CWE193_char_declare_ncpy   |!| one-byte off overflow |
| CWE805_char_alloca_loop    |C| enough stack space    |
| CWE805_char_alloca_memcpy  |C| enough stack space    |
| CWE805_char_alloca_memmove |C| enough stack space    |
| CWE805_char_alloca_ncat    |C| enough stack space    |
| CWE805_char_alloca_ncpy    |C| enough stack space    |
| CWE805_char_alloca_snprintf|C| enough stack space    |
| CWE805_char_declare_loop    |!| printLine() called with a overwritten pointer |
| CWE805_char_declare_memcpy  |!| printLine() called with a overwritten pointer |
| CWE805_char_declare_memmove |!| printLine() called with a overwritten pointer |
| CWE805_char_declare_ncat    |!| printLine() called with a overwritten pointer |
| CWE805_char_declare_ncpy    |!| printLine() called with a overwritten pointer |
| CWE805_char_declare_snprintf|!| printLine() called with a overwritten pointer |
| CWE805_int64_t_alloca_loop   |C| enough stack space/ infinite loop |
| CWE805_int64_t_alloca_memcpy |C| enough stack space |
| CWE805_int64_t_alloca_memmove|C| enough stack space |
| CWE805_int64_t_declare_loop   |!| printLongLongLine() called with a overwritten pointer |
| CWE805_int64_t_declare_memcpy |!| printLongLongLine() called with a overwritten pointer |
| CWE805_int64_t_declare_memmove|!| printLongLongLine() called with a overwritten pointer |
| CWE805_int_alloca_loop     |C| enough stack space/ infinite loop (overflowed data)|
| CWE805_int_alloca_memcpy   |C| enough stack space |
| CWE805_int_alloca_memmove  |C| enough stack space |
| CWE805_int_declare_loop    |!| printIntLine() called with a overwritten pointer |
| CWE805_int_declare_memcpy  |!| printIntLine() called with a overwritten pointer |
| CWE805_int_declare_memmove |!| printIntLine() called with a overwritten pointer |
| CWE805_struct_alloca_loop  |C| enough stack space/infinite loop (overflowed data) |
| CWE805_struct_alloca_memcpy|C| enough stack space    |


- O: shadow stack correctly protects return address 
- !: needs source code modification to handle it
- C: compiler issue: it's now impossible to overwrite retaddr due to compiler
- X: conceptually impossible to overwrite return addresses 

