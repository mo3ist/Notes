Controlling the flow is simply changing the EIP.
It's either **conditional** or **unconditional**

#### Unconditional flow control
`jmp	0x0004ff1b`
Change the EIP to an address without any conditioning, [[Instructions#jmp|jmp]] just does it.

#### Conditional flow control
`jcc	0x0004ffb1`
Change the EIP based on some condition. The condition's result is determined by the [[Registers#FLAGS|FLAGS]] register. The flags get set in most cases with the instruction *cmp* or *test*. And instructions that check for the flags are the variants of the *[[Instructions#jcc|jcc]]* instruction.
