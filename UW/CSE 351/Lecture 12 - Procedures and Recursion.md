## Stack Frame Details
- Typical stack frame layout:
	- Return address, which is pushed onto the stack by the call instruction, marks the beginning of the stack frame
	- `%rbp` was used, in older assembly code, as the frame pointer (where the current stack frame starts)
	- Old register values that needed to be saved would be pushed, along with local variables
	- If this procedure calls another procedure, it may need to push more register values and then arguments 7+ onto the stack
- Every stack frame is organized the same way, but each frame can be a different size to accommodate either additional information or eliminate redundancies 

![[Pasted image 20241020121119.png]]

## x86-64 Register Saving Conventions
- Describe how we should deal with register re-use to avoid destroying another procedure's data
- Two types of saving:
	- Callee-saved
	- Caller-saved
- Callee-Saved Registers
	- Callee's responsibility to save and restore the old value before using/manipulating the register
	- Saving is one of the first things done, and the restoring is one of the last 
	- The caller assumes the callee saves and restores the modified registers appropriately
- Caller Saved Registers
	- Caller's responsibility to save and restore (after the callee returns) the old value 
	- Callee has complete freedom to change registers since it can assume the caller has saved anything it needs later
- Any saved registers are part of the "Saved Registers and local variables" section of the stack frame

## Stack Frame Details
- A procedure needs to grow its stack frame in the following situations:
	- It has too many local variables to hold in caller-saved registers - will save old values of callee-saved registers
	- It has local variables that can't fit in registers - these must have space allocated for them in the stack
	- It uses the `&` operator to compute the address of a local variable - registers don't have addresses
	- It calls another function that takes more than 6 arguments
	- It uses data in caller-saved registers across a procedure call
	- It modifies/uses callee-saved registers

[[Lecture 11 - Stack and Procedures]]
[[Lecture 1 - Introduction, Binary]]