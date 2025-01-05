## Bitwise Operators
- AND (&): Outputs 1 when both bits are 1
- OR (|): Outputs 1 when one bit is 1
- XOR (^): Outputs 1 when *only* one bit is 1
- NOT (~): Outputs the opposite of its input
- Don't confuse with logical operators such as (OR `||`, AND `&&`, and NOT `!`)

## Unsigned Integers
- Represent non-negative integers
- `unsigned char`: 1 byte
- `unsigned short`: 2 bytes
- `unsigned int`: 4 bytes
- `unsigned long`: 8 bytes
- Range: $[0, 2^w - 1]$

## Signed Integers
- Represent both positive and negative integers
- Negative numbers are implemented via Two's Complement
- Most significant bit is marked negative 
- Advantages:
	- Zero has the encoding of all zeros 
	- It represents roughly the same number of positive and negative numbers 
	- The encodings for the positive numbers exactly match the encodings in unsigned
	- It has the following negation procedure: `-x = ~x + 1` (“flip the bits and add one”)
- Range: $[-2^{w - 1}, 2^{w - 1} - 1]$



**Sign and Magnitude Representation**: First bit tells the sign (1 for negative, 0 for positive) and the rest of the bits give the magnitude of the number
- Problems: Two representations of zero, weird arithmetic
## Bit Masks
- Binary operators are used with one sit of bits being the input and the other operand being a "bitmask" that performs a specific function
- Examples
	- `b & 0 = 0` 
	- `b & 1 = 0`
	- `b | 0 = 0`
	- `b ^ 0 = 0`
	- `b | 1 = 1`
	- `b ^ 0 = b`\
	- `b ^ 1 = ~b`
- [[Lecture 1 - Introduction, Binary]]

**Short Circuit Evaluation**: If the result of a binary logical operator can be determined by one operation, then the later operands are not evaluated in the first place

