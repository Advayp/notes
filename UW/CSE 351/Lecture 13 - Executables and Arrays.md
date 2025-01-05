## CALL
- Process of building and running an executable has four phases: compiling, assembling, linking, and loading (CALL)
- Compiling
	- Translates source code into assembly 
- Assembling
	- The assembler converts a text file of assembly into a binary object file (broadly defined as incomplete machine code
	- This is incomplete because we lack the addresses associated with labels - object file needs to be patched up with all the addresses once they're known
- Linking
	- Stitches together all the object and static library files needed to produce the final executable
	- Tries to resolve all references by looking through all the available symbol and relocation tables
	- Any unresolved references will cause linking to fail
- Loading
	- Takes an executable file and starts a running process from it
	- This sets up its memory sections and initializes the values of the registers
- Disassembling
	- Because ISA is so strict, we can work backwards and create assembly from binary files

## Arrays in Assembly
- Name of an array is just a placeholder for the starting address of the array
- Example of an array in assembly:
```
arr:
	.long 9
	.long 8
	.long 7
```
- The `.long` here means 4 bytes wide, just like the `l` width specifier
- Accessing elements:
	- `(Rb, Ri, S)` - with `Reg[Rb]` holding an address, `Reg[Ri]` holding an index, and `S` being the `sizeof(T)`
	- `D(,Ri,S)` - where `D` is the label of the array, `Reg[Ri]` has an index, and `S = sizeof(t)`
- Multidimensional arrays are stored in one big contiguous chunk of memory, so each element can be accessed with one dereference operation
- Multilevel array: created by adding extra levels of arrays of pointers to arrays. Each individual array uses contiguous memory, but allocated extra levels takes up more space in total and requires an extra memory access operation
[[Lecture 12 - Procedures and Recursion]]
[[Lecture 1 - Introduction, Binary]]