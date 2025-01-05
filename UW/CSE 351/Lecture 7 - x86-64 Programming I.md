## Instruction Set Architectures
- Combination of parts in a processor that one needs to understand to write assembly code
- Consists of the following:
	- System's State: The information that defines the culmination of past instructions
	- Instruction Set: List and format of all instructions the CPU can execute
	- The effect on the system state of each instruction
- Two main design philosophies
	- Complex Instruction Set Computer
		- Continue to add more specialized instructions over time as needed
		- Good for programmers, bad for hardware engineers
	- Reduced Instruction Set Computer
		- Restrict the ISA to a small set of instructions
		- Harder for programmers as longer tasks now consist of a lot of small instructions
- Contract or blueprint between hardware and software



## x86-64 Instructions
- Instructions are specified using a short instruction name followed by 0-3 operands, separated by commas
- Sample format
	- `instr op`
	- `instr src, dest`
- Three main categories
	- Data transfer
	- Arithmetic and logic operations
	- Control flow
- Each instruction includes a size specifier 
	- `b` for 1 byte
	- `w` for word (2 bytes, not the word size on your machine)
	- `l` for long word or 4 bytes
	- `q` for quad word, or 8 bytes

## x86-64 Operands
- Immediates: Constant integer data, prefixed with `$`
- Registers: the name of any 16 general purpose registers, prefixed with `%`
- Memory: a specified address that is dereferenced using `()`, which supersede the `%` inside them
- For instructions with two operands
	- Cannot use an immediate as your destination
	- Both operands can't be memory

## x86-64 Registers
- Stores a small amount of data (word size) that can be accessed very quickly
![[Pasted image 20241007234203.png]]
- Register names are given to word size data as well as smaller divisions

## Memory Addressing Modes
- Displacement (D = 0): displacement value, must be an immediate or constant
- Base Register (Rb = 0): name of the register that acts as the base of our calculation
- Index Register (Ri = 0): name of the register whose value will be scaled and added to the base
- Scale Factor (S = 1): Scales the value in Ri by either 1, 2, 4, or 8
- Computed Address is `Mem[ Reg[Rb] + Reg[Ri] * S + D ]`
- The operation takes the form `D(Rb, Ri, S)`

## Assembly Programmer's View
- Programmer-visible state
	- PC: the program counter (`%rip` in x86-64)
	- Named registers, which are together in a register section, store heavily used program data
	- Condition codes
		- Store status information about the most recent arithmetic operation
		- used for conditional branching

## x86-64 Assembly "Data Types"
- Integral data of 1, 2, 4 of 8 bytes
	- Data values
	- Addresses
- Floating point data of 4, 8, 10, or 2x8, 4x4, or 8x2
	- Different registers for those
	- Come from extensions to x86
	- Not covered in 351
- No aggregate types such as arrays or structures, just contiguously allocated bytes of memory
- Two common syntaxes
	- AT&T: used by our course, slides, textbook, and gnu tools (`operation src, dst`)
	- Intel: used by intel documentation, intel tools, etc. (`operation dst, src`)
	- **Must know which you're reading**

## Registers
- Can be accessed very quickly, store a small amount of data
- Have names prefixed with `%r`

## Moving Data
- General form: `mov_ src, dst`
- More of a copy than a move
- The `_` is the size specifier (b, w, l , q)

## More Instructions
![[Pasted image 20241009152148.png]]


[[Lecture 1 - Introduction, Binary]]
[[Lecture 2 - Memory and Data 1]]
[[Lecture 3 - Memory and Data 2]]
[[Lecture 8 - x86-64 Programming II]]
