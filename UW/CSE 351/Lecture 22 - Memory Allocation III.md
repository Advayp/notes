
## Garbage Collection
- Automatic memory management used by implicit dynamic memory allocators to reclaim heap-allocated memory
- Adds convenience for the programmer, but is computationally expensive
- Goal is to find out when a piece of dynamically allocated memory can be freed
	- Uses a directed graph 
	- Each allocated heap block is a node in the graph
	- Each pointer is an edge in the graph
	- Locations not in the heap that contain pointers into the heap are called root nodes
- Assumptions
	- Memory allocator knows which data are pointers and which are not
	- all pointers to the heap nodes point to the start of the payload
- Mark and sweep
	- One implementation of garbage collection
	- Uses an extra bit called the mark bit, which is stored similarly to the isAllocated bit in the boundary tags
	- Process
		- Recursively follows all of the root nodes into the heap and sets the mark bit for all reachable heap blocks
		- Sweeps through the heap from start to finish and check the mark bit for each block
			- If the mark bit is set, then clear it and move on
			- If it isn't set, then free the block since it's unused









[[Lecture 1 - Introduction, Binary]]