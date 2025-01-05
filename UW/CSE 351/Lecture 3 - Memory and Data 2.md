- Builds off [[Lecture 2 - Memory and Data 1]]


## Box and Arrow Diagrams
- Easy to visualize memory, data addresses are storing, and where pointers are pointing

**Pointer Arithmetic**: Takes the size of the data type being pointed to and automatically scales the operation and applies it to the original address
- [[Lecture 1 - Introduction, Binary]]

## Arrays
- Sets of contiguous memory that store the same type of data object
- Syntax `type array_name[num]`
	- Allocates `sizeof(type) * num` bytes of memory
- Can use square brackets to index into the array or simple arithmetic, like `array + n`
	- Shouldn't do the latter though bc of no bounds checking in either the positive or negative direction
- [[Lecture 2 - Memory and Data 1]]

## Strings in C
- Represented as arrays of characters
- End with a null character `\0` to signify the end of the string
- String literals are explicitly defined and are immutable 
	- Memory is properly allocated for these
