## Signed vs. Unsigned Integers
- Umin: Minimum value of an unsigned integer. This is always 0
- Umax: Maximum value of an unsigned integer. This is $2^w - 1$ 
- Tmin: Minimum value of a signed integer. This is $-2^{w - 1}$
- Tmax: Maximum value of a signed integer. This is $2^{w- 1} - 1$
- [[Lecture 4 - Data III, Integers I]]

## Casting in C
- Implicit casting done automatically by the compiler when there's a type mismatch during assignments or function calls (e.g,. when setting a signed variable to an unsigned variable, or vice versa)
- Casting between signed and unsigned integers doesn't change the representation of the data, just the interpretation
- When casting from a shorter integer type to a longer integer type:
	- For unsigned, we pad with zeroes
	- For signed, we pad with the most significant bit to maintain the sign of the original data
- Unsigned takes precedence when operating on both signed and unsigned integers
	- If you have two signed values, no casting is done (operation is performed while interpreting both values as signed)
- You can use `u` to force unsigned, such as `0u` or `1231243u`


## Sign Extension
- If we're casting a signed value to a version with a larger number of bits, we extend with the most significant bit to preserve the sign
- [[Lecture 4 - Data III, Integers I]]

## Two's Complement Arithmetic
- Same addition procedure works for both unsigned and two's complement integers
- Simplifies Hardware: only one algorithm for addition
- Algorithm: simple addition, discard the highest carry bit
	- Result is sum modulo $2^{w}$
	- Overflow occurs when the end result (without modulo) is not in range for the unsigned/signed integer
	- Number can't be represented in the current encoding scheme
	- C and Java ignore overflow exceptions
- [[Lecture 4 - Data III, Integers I]]

## Shift Operations
- Throw away extra bits that "fall off" the end
- Left shift (`x << n`) bit vector x by n positions
	- Fill with `0's` on right
	- Equivalent to multiplying by $2^n$
- Right shift (`x >> n`) bit vector by n spaces
	- X is unsigned: pad with zeroes on right (logical shift)
	- X is signed: pad with MSB on right (arithmetic shift)
- Shifting is faster than general multiply and divide operations
	- Shifts by `n < 0` or `n >= w` are undefined
- [[Lecture 1 - Introduction, Binary]]