
## Buffer Overflow
- Buffer: region of memory temporarily used to store data, typically an array
- Buffer overflow involves writing data past the end of a buffer and overwriting adjacent memory locations. This is possible because natively C has no bounds checking
- In certain cases, this can enable users to execute malicious code

## Stack Smashing
- This involves writing past the end of a local array in the stack
- Since array elements are laid out in increasing address order, stack smashing naturally moves toward higher addresses
- This allows us to rewrite the return address in the current stack frame

## Vulnerable Code
- Older libraries, especially those dealing with input, don't have bounds checking for the provided input
	- They keep writing to the buffer not until the buffer is full, but until they encounter a newline or end of file character
- This implies that we can change the input length such that it overflows the buffer 

## Code Injection
- Using buffer overflow to write instructions into the buffer and then modify the return address to execute the injected code

[[Lecture 1 - Introduction, Binary]]