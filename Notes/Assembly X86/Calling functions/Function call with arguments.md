Building upon [[Calling conventions#CDECL]] and [[Function call with no arguments]]:
#### The C code
![[CCode.png.png]]
It's just a simple program that does nothing but passing some arguments; firstname, lastname from *main*'s *argv* to *id*'s arguments.

#### The Assembly code
64 bits sorry :'(
![[AssemblyCode.png.png]]

#### The execution
![[Pasted image 20210215115454.png]]

#### The stack
*main*'s arguments on the stack: 
![[Pasted image 20210216025213.png]]
This is what's at the array pointer *argv*
![[Pasted image 20210215120306.png]]

*id*'s arguments: 
![[Pasted image 20210216025057.png]]

#### The explanation 
1- Before calling a function, the caller puts the arguments needed for the callee on the stack. They'll be under the calling address. 
2- The arguments are layed on the stack **from right to left**; Meaning the first argument is on the top of the stack, and the last argument is at the bottom. 
3- There're a lot of ways to access these arguments -read [[Addressing forms]] to see how to access the content of a memory address, but the facts are:	
* The arguments will be layed **from right to left**
* The first argument will be the one right **before the return address**

