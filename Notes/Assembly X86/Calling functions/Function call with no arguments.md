#### CDECL Assembly
```
call	function
...
# function
push	ebp 
mov		ebp, esp
...
mov		esp, ebp
pop		ebp
ret
```
`call	function` **pushes the *next* EIP** to the stack, then  **changes the EIP** to the address of another sub-routine (`function`).

`push	ebp` **links to the stack frame of the previous subroutine/function** so we can go back to it when we're done. It subtracts 4 from the ESP.
 ^12d231

`mov		ebp, esp`  puts the ESP -which is a **reference to the new function's stack frame**- in EBP so we can use it for the function's arguments and local variables. 

`mov 	esp, ebp` is just a way to clean up the stack frame back to the base pointer. That way we don't worry about the local stuff made in the function. 

`pop	ebp` adds 4 to the ESP, Then puts whatever is at the top of the stack into EBP.

`ret` is basically a `pop` into EIP. It pops the address on the top of the stack into EIP. So it **returns to where it left the caller**.