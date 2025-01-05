
## Extension Instructions
- Similar to a regular `mov` instruction
	- But source is smaller than destination
- Format `movz[src size][dest size]`
	- pads with zeroes (hence the z)
- Format `movs[src size][dest size]`
	- pads with the MSB (hence the s)

## Conditionals
- Two main parts
	- An instruction that sets/changes the condition codes (arithmetic, logical, cmp, test)
	- A conditional jump instruction (that compares everything to zero)

## Labels
- Operand to a jump instruction is known as a label
- Examples: `main:`, `foo:`, `loop:`
[[Lecture 8 - x86-64 Programming II]]
[[Lecture 1 - Introduction, Binary]]