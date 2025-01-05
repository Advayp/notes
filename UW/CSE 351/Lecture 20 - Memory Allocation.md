## Dynamic Memory Allocators 
- Allocation requests are only known and their sizes are only known at runtime
- Two types of allocators:
	- **Implicit**: programmer is only response for allocations and the allocator implicitly handles deallocations (e.g, Java)
	- **Explicit**: Programmer is responsible for allocations and deallocations (eg., C)
- Allocator Interface:
	- Applications
		- Can issue a series of allocations and deallocations
		- Must never access memory that's not allocated
		- Must never deallocated memory that's not allocated
	- Allocators
		- Can't control size of allocated blocks
		- Must respond immediately to allocation requests
		- Must satisfy alignment requirements
		- Can only allocate from freed memory
		- Can't move allocated blocks
- Performance Goals:
	- Throughput: Complete as many allocation and deallocation requests as possible per unit time
	- Memory utilization: using heap space as efficiently as possible
- Allocator Implementations
	- Implicit free list: traverses its blocks via arithmetic by using the size of each block
	- Explicit free list: traverses its free blocks using a linked list

## Heap Fragmentation
- **Internal fragmentation**: wasted space inside of allocated heap blocks
	- Payload: `size` in `malloc(size)`
	- Internal fragmentation is all the space within a block that's not the payload
	- Allocator typically allocates more space than necessary
- **External Fragmentation**: Unused space between allocated heap blocks
	- Holes **between** allocated blocks (must be between two allocated blocks)
	- Caused by the specific pattern of allocation and deallocation requests
	- Can cause situations where an allocation request cannot be satisfied despite there being enough total free memory

[[Lecture 1 - Introduction, Binary]]