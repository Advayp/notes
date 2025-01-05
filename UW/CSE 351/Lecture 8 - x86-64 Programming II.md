
## Address Computation Instruction
- Name: load effective address, denoted `lea`
- Source operator must be a memory operand and its destination operand must be a register operand
- Sample instruction:
	- `lea D(Rb,Ri,S), R`
	- This stores `Reg[Rb] + Reg[Ri] * S + D` in `Reg[R]`
- Example:
	- Assume `int* p` is stored in register `%rax`
	- Then, the operation `p += 1` can be achieved by writing the following
	- `lea 4(%rax), %rax`
- Arithmetic with `lea`
	- `lea` can be used to perform arithmetic computations that fit the address calculation format
	- Example:
		- `lea (%rdi,%rsi,4), %rax`
		- Assume x is stored in `%rdi`, y in `%rsi`, and z in `%rax`
		- If we have `int* x` and `long y`, then this is equivalent to `int* z = &x[y]`
		- If we have `long x` and `long y`, then this is equivalent to `long z = x + 4 * y`


## Condition Codes
- Status bits part of the CPU state that indicate information about the most recently executed assembly instructions
- Conceptualize as multiple single-bit registers, but they're actually smth else under the hood
- Four primary condition codes
	- Carry Flag (CF)
	- Zero Flag (ZF)
	- Sign Flag (SF)
	- Overflow Flag (OF)
- Set implicitly by arithmetic and logical operations and indicate whether or not the result had unsigned overflow (CF), was zero (ZF), was negative (SF), or had signed overflow (OF)
- Can also be explicitly set through compare (`cmp`) and `test`
	- These solely update the condition codes and their results are never stored
	- `cmp` produces a result equivalent to `sub`
	- `test` produces a result equivalent to `and`
- Their values are used to determine the outcome of two families of instructions, jump and set
- Jump and set allow us to implement all control flow


## Jump and Set
![[Pasted image 20241008174802.png]]


## Other Notes
- First argument of a function (in C) is always stored in `%rdi`, and the second is always stored in `%rsi`
- Return is in `%rax`



[[Lecture 1 - Introduction, Binary]]
[[Lecture 2 - Memory and Data 1]]
[[Lecture 3 - Memory and Data 2]]
[[Lecture 7 - x86-64 Programming I]]