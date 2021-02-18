#### EAX
Commonly used as the return value of functions

#### EBX 
Optional base pointer.

#### ECX 
Loop counter

#### ESI
Source address

#### EDI  
Destination address

#### ESP   
Stack pointer 

#### EBP  
Base pointer
	\- Points at the start of the stack frame of a function 
	\- It's a linked list; each EBP points to the previous function's EBP

#### FLAGS
The register with byte *flags* that get set after a certain instruction is executed to detect, for example, if the operation's resultant was *zero* or if it was signed or not ,etc...
Here's a table from Wikipedia with some EFLAGS
![[Pasted image 20210216101148.png]]
You should just be familiar with:
- **ZF**: Zero Flag, gets set every time the result is zero ^241926
- **SF**: Sign Flag, gets set every time the result is signed
- **CF**: Is set when the result of an operation overflows, for example, 0x10000000 + 0x10000000 = 0x00000000 and the OF will be 1. It's used to detect if there's an 'error' in a certain **unsigned** bits operation.  ^CF
- **OF**: It's used to detect an 'error' in a certain **signed** bits operation. It's set when the **sign bit is flipped**; if the sign bit of the operators were the same and the result was different, it will be set. ^OF