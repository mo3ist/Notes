#### CDECL

^bfabfe

Quoting Wikipedia
>In the CDECL calling convention the following holds:
\- Arguments are passed on the stack in **Right-to-Left order**, and **return values are passed in eax.**
\- **The _calling_ function cleans the stack. **This allows CDECL functions to have _variable-length argument lists_ (aka variadic functions). For this reason the number of arguments is not appended to the name of the function by the compiler, and the assembler **and the linker are therefore unable to determine if an incorrect number of arguments is used.**
\
Variadic functions usually have special entry code, generated by the va\_start(), va\_arg() C pseudo-functions.