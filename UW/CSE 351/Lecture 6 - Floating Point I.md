## Scientific Notation
- Numbers written in scientific notation are in the form `sign * mantissa * base^exponent`
	- The mantissa is a positive numeral 
	- In normalized scientific notation, the mantissa has exactly one nonzero digit to the left of the decimal point


## IEE 745 Floating Point Encoding
- Based on normalized binary scientific notation 
- Encodes the three components (sign, exponent, and mantissa)
![[Pasted image 20241005103201.png]]
- The single letter names, such as S, E, and M, refer to the binary encoding of the sign, exponent, and mantissa respectively
- Each float or double is evaluated in the following way (everything is in base 2, including the `1.M`):
$$
\text{sign} \cdot \text{mantissa} \cdot 2^{\text{exponent}} = (-1)^S \cdot 1.\text{M} \cdot 2^{E - \text{bias}}
$$
- Explanation of the `1.M`:
	- In normalized scientific notation, the mantissa must have exactly one positive digit to the left of the decimal point. In binary, the only option is 1, which is why we write `1.M`
- Sign Field (S)
	- Represented by a single bit (0 = Positive, 1 = Negative)
- Exponent Field (E)
	- Encoded in bias notation
	- Shifted by a value of $2^{w - 1} - 1$ (or one 0, followed by a series of ones panning the total bit width) and then converted to unsigned
	- This relationship can be expressed in two ways:
		- E = exponent + bias
		- exponent = E - bias
- Mantissa Field (M)
	- Only store the first bits after the binary point, padding with trailing zeroes as necessary
	- If the mantissa without the trailing zeroes is longer than the bit width, it's impossible to represent the exact value, which leads to rounding errors

## Normalized Floating Point Conversions
- Floating Point to Decimal
	- Append the bits of M to the leading one to form the mantissa
	- Multiply the mantissa by $2^{E  - \text{bias}}$
	- Multiply that result by the sign
	- Multiply the exponent by shifting the binary point
	- Convert to decimal
- Decimal to Floating Point
	- Convert from decimal to binary 
	- Convert to normalized binary scientific notation
	- Encode the sign as 0 or 1
	- Encode E as the exponent + bias in unsigned
	- Encode the 23 bits after the binary point, padding with trailing zeroes as necessary, in M

## Limitations
- can only *exactly* represent numbers in the form $x \cdot 2^{y}$
- Other rational numbers have repeating bit representations, like `1/3` in decimal 

## Special Cases
- If `E` and `M` are all zeroes, the float evaluates to zero
- Two zeroes exist (+0, -0)\
- If `E = 0xFF` and `M = 0`, the float evaluates to positive or negative infinity (based on the sign bit)
- If `E = 0xFF` and `M != 0`, the float evaluates to `NaN`
	- The result of computations such as `0/0`, square root of a negative number, or inf/inf
	- Propagates throughout computations

## New Representation Limits
- New largest value
	- `E = 0xFE` has largest
- New numbers closest to zero
	- Smallest exponent is `E = 0x01`
- Denormalized numbers
	- `E = 0`
	- Instead of the leading one in the mantissa, denormalized numbers have a `0` before, allowing us to get closer to zero

## Distribution of Values
- What ranges are not representable?
	- Between largest norm and infinity (overflow, exp too large)
	- Between zero and smallest denormalized number(underflow, exp to small)
	- Between norm numbers (rounding)

## Mathematical Properties of FP Operations
- Overflow yields infinity and underflow yields 0
- Floating point operations do not work like real math, due to rounding
	- Not associative, distributive, or cumulative
- Repeatedly adding a very small number to a large one may do nothing, because the result may not fit in the mantissa
- Compare two floating point numbers using some arbitrary epsilon instead of direct comparison

# Floating Point Arithmetic
- Addition/Subtraction
	- Shift the exponent of the smaller number so that it matches the larger one
	- Line up the binary points of the mantissas
	- Perform the operation
	- Encode the result in a floating point
- Multiplication
	- Sum the exponents
	- Multiply out the mantissas
	- Encode the result in a floating point (possibly to a special case)
	

## Connections
[[Lecture 5 - Integers II]]
[[Lecture 1 - Introduction, Binary]]
[[Lecture 4 - Data III, Integers I]]