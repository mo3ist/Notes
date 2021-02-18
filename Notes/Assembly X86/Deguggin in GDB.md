It's a Linux debugger. So you'll use it for ELF file format.
#### Usage
Don't use vanilla GDB.  Use it with [peda](https://github.com/longld/peda).
- **help**
	For getting help generally or on some command    

- **run** \<args>
	Running the program with optional arguments.
	You can redirect bash commands to stdin like this
	```
	bash $ python -m "print('arg')" > input_file
	bash $ gdb
	gdb $ run < input_file
	```

- **break** \<subroutine>, **break** \*\<address>
	To set break points on a function like main `break main` or on some address like `break *0x565561ad`
	
- **/**\<format>
	Used with **print** and **x** commands to format their output 
	Quote:
	>Format letters are o(octal), x(hex), d(decimal), u(unsigned decimal),
  t(binary), f(float), a(address), i(instruction), c(char), s(string)

- **print**/\<format>
	Print something as it is, like for example the content of a register
	`print/x	$eax`
	
- **x/** \<address\>
	Examine memory at **address**
	`x/s	0x00041ff0` to print what's in memory at address 0x00041ff0 as a string.

- **disassemble** 
	To disassemble functions
	`disassemble main`

- **ni**
	Step forward and skip subroutines

- **si**
	Step forward and don't skip subroutines
	
	