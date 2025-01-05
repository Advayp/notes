
## Memory Layout
![[Pasted image 20241016165400.png]]

## The Stack
- Section of memory that takes up the highest useable addresses
- Holds local variables and other procedure context
- Grows downwards

## The Stack Pointer
- End of the stack is stored in `%rsp`
- It holds the lowest address (the most recently pushed element)
- Moves as the stack is manipulated
## Stack Manipulation
- Stack pointer can be changed directly via `subq` and `addq`, but this doesn't do anything with the underlying data
- Transfer data to and from the stack using `push` and `pop` instructions
- `push` will:
	- Decrement `%rsp`
	- Copy the data from the source operand into the newly-allocated space
- `pop` will
	- Copy the data from `%rsp` into the destination operand and then increment increment `rsp` to deallocate that space

## x86-64 Calling Conventions
- Caller: procedure doing the calling
- Callee: the procedure being called
- Return address
	- Store a return address on the stack, which holds the address of the caller's next instruction to execute
- Procedure call (`call`)
	- Passes control to another procedure
	- Automatically pushes the return address onto the stack and updates the program counter to the address of the specified label
- Procedure return (`ret`)
	- Automatically pops the return address off of the stack
	- Updates the program counter to the popped address
	- The return address stores the address of the instruction to execute after the callee returns
- Procedure Data Passing
	- First six arguments are placed in: `%rdi, %rsi, %rdx, %rcx, %r8, and %r9`
	- Return value `%rax`

![[Pasted image 20241018145842.png]]
- Be careful when referring to arguments (7+) from the stack pointer, since the return address is pushed to the stack as well. 
	- For example, to access the 8th argument, you would use `16(%rsp)`, because you need to go up 8 bytes to the 7th argument and then 8 bytes again to the 8th argument

## Stack Based Languages
- Languages that support recursion
	- Code must re-entrant: multiple simultaneous instantiations of single procedure
	- Need some place to store state of each instantiation
- Stack allocated in frames
	- State for a single procedure instantiation
- Stack discipline
	- State for a given procedure needed for a limited time
	- Callee always returns before caller does

[[Lecture 10 - x86-64 Programming IV]]
[[Lecture 1 - Introduction, Binary]]