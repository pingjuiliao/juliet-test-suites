## This branch test codes that are protected by shadow stack.
We are only interested in return address overwrite

## CWE121: Stack_Based_Buffer_Overflow

###how I run each testcase
```
# in each directory: e.g <repo>/testcases/CWE121/s01 
make individual
```

### Results:
- O: shadow stack correctly protects return address 
- !: needs source code modification to handle it
- C: compiler issue: it's now impossible to overwrite retaddr due to compiler
- X: conceptually impossible to overwrite return addresses 

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
| CWE805_int_alloca_loop       |C| enough stack space/ infinite loop (overflowed data)|
| CWE805_int_alloca_memcpy     |C| enough stack space |
| CWE805_int_alloca_memmove    |C| enough stack space |
| CWE805_int_declare_loop      |!| printIntLine() called with a overwritten pointer |
| CWE805_int_declare_memcpy    |!| printIntLine() called with a overwritten pointer |
| CWE805_int_declare_memmove   |!| printIntLine() called with a overwritten pointer |
| CWE805_struct_alloca_loop    |C| enough stack space/infinite loop (overflowed data) |
| CWE805_struct_alloca_memcpy  |C| enough stack space    |
| CWE805_struct_alloca_memmove |C| enough stack space    |
| CWE805_struct_declare_loop    |!| printStructLine() called with an overwritten pointer |
| CWE805_struct_declare_memcpy  |!| printStructLine() called with an overwritten pointer |
| CWE805_struct_declare_memmove |!| printStructLine() called with an overwritten pointer |
| CWE806_char_alloca_loop     |!| printLine() called with an overwritten pointer |
| CWE806_char_alloca_memcpy   |!| printLine() called with an overwritten pointer |
| CWE806_char_alloca_memmove  |!| printLine() called with an overwritten pointer |
| CWE806_char_alloca_ncat     |!| printLine() called with an overwritten pointer |
| CWE806_char_alloca_ncpy     |!| printLine() called with an overwritten pointer |
| CWE806_char_alloca_snprintf |!| printLine() called with an overwritten pointer |
| CWE806_char_declare_loop    |!| dst buffer allocated after large src buffer |
| CWE806_char_declare_memcpy  |!| dst buffer allocated after large src buffer |
| CWE806_char_declare_memmove |!| dst buffer allocated after large src buffer |
| CWE806_char_declare_ncat    |!| dst buffer allocated after large src buffer |
| CWE806_char_declare_ncpy    |!| dst buffer allocated after large src buffer |
| CWE806_char_declare_snprintf|!| dst buffer allocated after large src buffer |
| dest_char_alloca_cat        |C| enough stack space                          |
| dest_char_alloca_cpy        |C| enough stack space                          |
| dest_char_declare_cat       |!| printLine() called with an overwritten pointer |
| dest_char_declare_cpy       |!| printLine() called with an overwritten pointer |
| placement_new_alloca        |!| class size not large enough/ cpp            |
| placement_new_declare       |!| class size not large enough/ cpp            |
| src_char_alloca_cat         |!| printLine() called with an overwritten pointer |
| src_char_alloca_cpy         |!| printLine() called with an overwritten pointer |
| src_char_declare_cat        |!| dst buffer allocated after large src buffer |
| src_char_declare_cpy        |!| dst buffer allocated after large src buffer |

### Some pattern :
- CWE129: arbitrary write
- CWE805: sequential buffer overflow (choosing wrong buffer)
- CWE806: sequential buffer overflow (wrong size)
- *_alloca_* : depreciated alloca() function, compiler tends to allocate enough stack space to handle it 
- *_declare_*: char[]
- _wchar_    : for windows, not handled in linux perhaps
- *_01~84_*  : often, 1 to 68 is c files, after 70 is cpp file, 

### Conclusion
many testcases cannot survive the function call because the stack buffer overflow overwrites critical data.


## Other potential errors
|Interested?|Name| Reason | 
|-----------|----|------------------|
|X|CWE562_Return_of_Stack_Variable_address| it's about returning a stack allocated buf/struct|
|X|CWE680_Integer_Overflow_to_Buffer_Overflow| malloc/new operation are exclusively included in this class|

