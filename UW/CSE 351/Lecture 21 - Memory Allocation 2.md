## Allocation Strategies
- **First Fit**: find the first block that is large enough
- **Next fit**: Search the list starting from where the first search finished and return the first valid free block (with wrap around at the end of the heap)
- **Best fit**: Search the whole list and return the free lock that is best (large enough and minimizes external fragmentation, with some way of breaking ties)

## Allocating A Free Block
- Compute the necessary block size, based on payload, metadata, and padding
- Search for a suitable free block using the allocation strategy
	- if not found, return NULL
- Compare the necessary block size against the size of the chosen block
	- If equal, continue
	- If not, split off the excess and convert into a new free block
- Allocated the block and return the address of the beginning of the payload

## Alignment 
- Address of the beginning of the payload must be a multiple of the alignment size
- Total size of the block will be padded out to be a multiple of the alignment size

## Minimum Block Size
- Each allocated block must include metadata and satisfy alignment requirements, which means there's a minimum block size
- This affects the computation of the necessary block size and splitting
	- Even if the request is very small, the computed necessary block size will be padded out to the minimum block size
	- If the remaining free space after splitting is less than the minimum block size, then it will be included as padding in the allocated block

## Freeing an Allocated Block
- Free by flipping its `is-allocated` flag
- However, we also need to coalesce neighboring free blocks into a single, larger free block. This maximizes the ability of the allocator to fulfill larger allocation requests

## Coalescing
- Use the header to traverse to following blocks, and, if they're free, merge
- To reach the blocks behind the ones currently being freed, we add a footer to each block containing the same information as the header
- The header and the footer together are known as boundary tags


[[Lecture 1 - Introduction, Binary]]