#### What are the disassembled instructions
The instructions we see in the disassemblers are the translation of the byte sequences of the binary. The key point in disassembling is reading with the correct offsets in mind. For example, by examining the memory at an address with just 1 byte simply shifted, the instruction completely changed:
![[Pasted image 20210218172824.png]]
`lea	ecx, [esp+4]` magically became `dec		esp`.

#### Disassembling methods
There are 2 methods of disassembling a binary:
- Linearly -> Disassembling one instruction after another (e.g. **GDB**).
- Recursively -> Following the jumps (e.g. **IDA**).


#### Abusing static analysis
- Since a simple shift can miss up a good portion of the next chunk of instruction, if we can trick the dissembler into shifting those bytes for us, by for example, executing a fake `call` instruction with a **3-byte-address instead of 4** to make the disassembler read the next byte of instructions as if it was the remainder of the address, that will miss up some code. 
  The only way we can make this work without corrupting the binary is to put these fake instructions in places where they won't get executed, like after a non-conditional jump instruction or something.
- Another way to waste the analyst's time is by **branch functions**. It's a technique where you don't jump to things directly but instead direct all the jumps into one block of code (a function) that does some calculations then jumps for you indirectly. This way the Control Flow Graph won't help the analyst that much 'cause a lot of the jumps will be directed into one place.
-  Yet another technique is to take a chunk of code then scramble it into small unordered pieces with a lot of jumps. 