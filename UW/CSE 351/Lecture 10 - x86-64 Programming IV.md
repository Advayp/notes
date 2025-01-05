
## Loops
 - Can be constructed using labels and jump statements
 - Jump statements must go back to the the beginning of the loop body
 - Differences in loops
	 - When you evaluate the test conditional (top or bottom of the loop)
	 - Efficiency in terms of the number of jump instructions you need to evaluate
 - Do while loop
```
loopTop:
	<body code>
	<CC instr>
	j* loopTop
```
- While Loop
```
loopTop:
	<CC instr>
	j*' loopDone
	<body code>
	jmp loopTop
```
```
	<CC instr>
	j*' loopDone
loopTop:
	<body code>
	<CC instr>
	j* loopTop
loopDone:
```

## Switch Statements
- Can be thought of as a specialized syntax for chains of if-else statements
- Jump table: data structure used to help branch to different parts of a program
- An array of pointers that point to instructions that should be executed if a given condition is satisfied
- Program counter: special register that holds the address of the next instruction. Normal behavior is to advance between consecutive instructions, but jump instructions can alter this behavior 
- Indirect jumps:
	- To use the jump table, we must update the program counter to one of the addresses stored in the table
	- Syntax: `jmp *Loc`
	- Example: `jmp *.L4(,%rdi,8)`
		- Updates `%rip` to the address of the appropriate code block 

[[Lecture 9 - x86-64 Programming III]]
[[Lecture 1 - Introduction, Binary]]