## Introduction 
- Divide work between multiple threads and synchronize behavior
- Allows us to solve problems faster than we could earlier, since now multiple things can happen at the same time

## Parallelism vs. Concurrency
- Parallelism: use extra resources to solve your problem faster
	- To cut a bunch of potatoes, get 20 other cooks to cut the potatoes too
- Concurrency: Use a single resource among multiple threads
	- Manage shared resources, like 10 cooks are trying to share 4 burners.
- Parallel Code with threads
	- Each thread has its own program counter and its own stack
	- Share objects and static fields (heap memory)
	- Threads communicate by altering memory

## Fork/Join
- Fork: start a new thread and start the execution
- Join: Wait until the thread stops executing, block execution of main until the joined thread is done executing