# The all-mighty manual
[Intel manual](https://software.intel.com/content/www/us/en/develop/download/intel-64-and-ia-32-architectures-sdm-combined-volumes-1-2a-2b-2c-2d-3a-3b-3c-3d-and-4.html) that you'll probably won't open and will resort to StackOverflow instead :)


#### push
`push	source`
- It's main usage is to **push source on the top of the stack & subtract 4 from the ESP**
- It can also be used similar to `sub	esp, 4` to reserve some space on the stack for a local variable (but then you'll have to `add	esp, 4` to keep the stack clean).

#### pop
`pop	destination`
- Puts whatever is on the top of the stack into *destination* and it adds 4 to ESP

#### mov
- mov
`mov	r/m32, source`
Copies the source to the destination. Like saying `r/m32` = `source`.

#### lea
`lea	destination, [source]`
- It calculate the value of *source* (if *source* for example was `[ebp+ecx*4+1]`) then puts it into *destination*. It doesn't load the content of memory at *source*, it just loads the address.
- Since it calculates the *source* expression, it can be used to do quick simple math in the CPU registers instead of doing it on memory

#### call
`call	subroutine(0x00000001)`
- Pushes the next EIP address to the stack then changes the EIP to the suproutine's address.  

#### ret
`ret` | `ret	value`
- It's similar to `pop	eip`; pops the return address pushed on the stack by `call`. 
- If it has a `value`, `ret` will add it to ESP so that it releases *value* bytes of memory (in stdcall calling convention) 

#### leave
`leave`
It's the combination of 
- `mov	esp, ebp` bring the stack back to the beginning of the frame
- `pop	ebp` pop back the previous saved EBP

#### cmp
`cmp	destination, source`
Compares `source` to `destination` to set the ![FLAGS](Registers#FLAGS) register. Either the source or the destination can be [[Addressing forms#r m32|r\m32]] or a *register*.

#### test
`test	destination, source`
Bitwise anding between source and destination, it can set the ZF bytes in [[Registers#FLAGS|FLAGS]]. It's used when the value of the anding isn't stored, it doesn't set the destination.

#### jmp
`jmp	address`
Changes the EIP to `address` thus changing the flow of the program.
 
#### jcc
`jcc	address`
They are a set of instructions, just like `jmp`, but when a certain condition is met. Some of them are:
- `je`(jump equal) / `jz` (jump zero)
- `jne` (jump not equal) / `jnz` (jump not zero) 
- `jg` (jump greater than):
- `jge` (jump greater than or equal)
- `jl` (jump less than)
- `jle` (jump less than or equal)

Just not to get lost by this trivial mistake, you can read `jge eax, edx` as `eax jge edx` (**EAX >= EDX**)

#### shl
`shl	destination, value`
shift the value at destination by `value` then put it in `destination`. 
- When destination get shifted to the left and there's an overflow or something (e.g. 0x11110000 << 4 = 0x1**11100000**) the [[Registers#^CF|CF]] (Carry flag) will be set. 
>At the end of the shift operation, the CF flag contains the last bit shifted out of the destination operand.

- Not only the carry bit, but also the [[Registers#^OF|OF]] bit can be set if the sign bit of `destination` was flipped. 

It's a **logical shift** by the way (meaning it adds 0's like a normal shift operation and doesn't care about 2's complement stuff ), so it work with **unsigned bits**.
It can represent multiplying `destination` by 2^`value`.

#### shr
`shr	destination, value`
Similar to `shl` but it shifts to the right. Also is a logical right shift.
It can represent dividing `destination` by 2^`value`.

#### imul
Signed multiplication.

- `imul	r/m32`
The destination here will be EDX:EAX concatenated, like a 64 bit register. It will multiply EAX by the `r/m32`

- `imul	reg, r/m32`
The destination will be EAX. It multiplies `reg` by `r/m32`.

- `imul	reg, r/m32, immediate`
The destination will be `reg`. It multiplies `r/m32` by `immediate`.

#### div
Unsigned division.

- `div	ax, r/m8`
The quotient destination will be `ah` and the remainder will be at `al`.

- `div	eax, r/m32`
The quotient will be at `eax` and the remainder at `edx`.

- Can't divide by 0

#### rep
It's not a family of instructions, but rather a family of prefixes; they *repeat string-operations until tested-condition*. They stop when the [[Registers#^CF|CF]] flag or the [[Registers#^241926|ZF]] flag matches the condition.
- `rep` repeat while equal
- `repnz` repeat while not zero
- `repz` repeat while zero


- `rep stos`: `rep stos dword ptr es:[edi]`
	- A quoted definition:
	> Repeat while zero: Transfer the contents of the EAX register to the memory double-word addressed in the destination register EDL, relative to the ES segment.

	- Basically what it does is :
		- **EDI** is the destination; it will be the reference that will hold the base memory address.
		- **EAX** will contain the literal data that will be put on memory
		- **ECX** will be the counter, meaning how many times is will copy EAX to memory. When it reaches 0, the next instruction in the code will be executed. 
		-  **So,** it will take whatever is in **EAX** then put it in `[edi + ecx*4 ]`.	After each instance in the repetition, it will decrement ECX and will stop when it's 0.
		-  Other than working with [[Sizes#Data sizes|size]] `dword`, it can work with `byte`; moving `al` into `[edi + ecx*1 ]`. 

	- Here's a little sketch I made:
	![[Pasted image 20210217092629.png]]


