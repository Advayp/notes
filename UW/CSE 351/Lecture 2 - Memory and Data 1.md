## Office Hours
- Allen Center (CSE1), mostly on the third floor

## CPU Execution Cycle
- Fetch the instruction
	- Controlled by hardware
- Fetch any data required by the instruction
- Perform the specified computation
- Write the result back to memory
- Instructions are temporarily held in the instruction cache (i-cache)
- Other data are held in registers
- The flow of data is controlled by the programmer (creating/using/storing variables)

## Definitions
- Most Significant Bit: Leftmost bit (changing it has a significant impact on the value stored)
- Least Significant Bit: Rightmost bit  (changing it has a small impact on the value stored)
- [[Lecture 1 - Introduction, Binary]]

## Fixed-Length Binary
- Everything is stored as a fixed length, with leading zeroes added to ensure the data fits the specified size
- Make sure to pad things out before computation
- [[Lecture 1 - Introduction, Binary]]

## Memory
- Memory is a single large array of bytes, each with a unique address/index
- Each address is a number represented in fixed-length binary (usually a byte)
- Domain of possible addresses = address space
- Not all values fit in a single byte, so multiple addresses are used

## Machine "Words"
- Word Size = Address Size = Register Size
- word size = w bits -> $2^w$ addresses
- Current x86 systems use 64bit words
	- [[Lecture 1 - Introduction, Binary]]

## Address of Multibyte Data
- Addresses still specify locations of bytes, but memory can be viewed as series of chunks of fixed-sized data
- Each chunk represents a different piece of data

## Endianness
- Consecutive bytes are stored in consecutive addresses
- Focus on the byte level, not bits
- Big-Endian: least significant byte has the highest address
- Little-Endian: least significant byte is stored in the lowest address


