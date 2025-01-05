## Overlaying a process
- The `exec*` family of functions overlays a process with a fresh instance of the specified program
- Starting state of the new program:
	- Data: static data and literals are copied from the program executable
	- Code: copied from the program executable
	- Heap: no dynamic memory requests are possible at this point
	- Stack: sets up main and handles any arguments passed into `exec*`
	- Register: values are setup so that the new process can execute properly

## Ending a process
- Executing the return statement from main (provide status code)
- Calling the library function exit (provide status code)
- Via an abort from the exception handler

## Process resources
- Every process consumes resources, in the form of the data it needs
- Data is also stored when context-switching occurs
- A zombie process is one who's data still exists in memory
- Reaping (deleting the data associated with a given process) occurs after termination
- Parent is responsible for reaping its child
	- Happens implicitly when the parent terminates
	- Explicitly using the `wait()` or `waitpid()`, which suspend execution until the child process terminates

## `init/systemd`
- Reaping only occurs on terminated processes 
- Usually a parent is responsible for reaping 

## Virtual Memory
- Virtual address space: the number of bytes each process thinks it has available
- Physical address space: the set of all bytes that must be shared between all currently running processes
- A region of the disk called the swap space is used to store excess memory
- Virtual memory works via a layer of indirection. Converts address from virtual memory to physical memory

[[Lecture 1 - Introduction, Binary]]