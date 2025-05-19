## Stacks And Queues
- Stacks - Array Implementation
	- Push: O(1) amortized, might need to resize
	- Pop: O(1)
- Stacks - LL implementation
	- Push: O(1)
	- Pop: O(1)
	- Main downside is chasing all the pointers, which can be expensive
- Queues - Circular Array Implementation
	- Maintain two pointers for head and tail. When dequeuing, just move heap up one index and mod the result by the array size
	- When inserting, move tail up one spot (mod table size, resizing if necessary) and insert the new element
	- Enqueue: O(1) amortized, might need to resize
	- Dequeue: O(1)
- Queues - LL Implementation
	- One pointer at the head of the LL, one at the tail
	- Enqueue: O(1)
	- Dequeue: O(1)

## Big Oh, Omega, and Theta
- Big Oh: Upper bound for runtime, not necessarily tight. f(n) is O(g(n)) if there exists constants x and c such that for all n >= x f(n) <= c g(n)
- Big Omega; Lower bound for runtime, not necessarily tight.  f(n) is Omega(g(n)) if there exists constants x and c such that for all n >= x f(n) >= c g(n)
- Big Theta: Tightest bound for runtime. f(n) is Theta(g(n)) if it is both O(g(n)) and Omega(g(n))
- These bounds apply to space complexity too
- When determining the runtime for code blocks, observe what happens as N gets very large.
- If necessary, write out all the operations being performed and obtain a closed form

## Recurrence Relations
- To find closed form, write out as a function. Then, draw the tree and sum the work for each level, starting from the root and ending at the leaf nodes.
- Use constants when necessary to write a recurrence relation for a code block
- Constants are necessary when doing some amount of arbitrary work in a loop (not related to input size) performing some basic operations like comparisons, addition, and subtraction


## Binary Heaps
- Structure
	- Tree is complete (last level is the only one that's not filled)
	- For a min heap, every child is greater than or equal to the parent
	- For a max heap, every child is less than or equal to the parent
- Perfect tree is when all levels are completely filled
- Insertion runtime:
	- Best Case: O(1), no need to percolate element up
	- Average case: O(log n)
- Find Min
	- All O(1)
- deleteMin
	- O(log n)
- increaseKey/Decrease Key
	- O(1) best case, no need to move element
	- O(log n) normally
- Remove
	- O(1) best case, element is a leaf 
	- O(log n) normally

## Dictionary ADT
- Insert, Find, Delete all self-explanatory

## Binary Search Trees
- Every node has at most 2 children
- Nodes in the left subtree are smaller, nodes in the right subtree are greater
- Find: pretty much binary search
- Insert: binary search your way to the insert spot, then insert
- Delete: find node if it exists, then replace with largest node in the left subtree or smallest node in the right subtree
- All log n on average. Degenerate cases can lead to O(1) runtime for best case
	- Insert: all right-tree, inserting node smaller than root
	- Finding: root is the node you're looking for
	- Deleting: All left-tree, replacing node with largest node in the right subtree


## AVL Trees
- Invariant:
	- The difference in height of the left and right subtree of a node is at most 1
- From this property, we get that the height is roughly log n
- Find runtime: O(log n) most cases, O(1) if the root is what you're looking for
- Insert runtime: O(log n)

## Hash Tables
- Good Hash Function
	- Minimizes collisions
	- Uses output space efficiently
	- If a == b, then hash(a) == hash(b)
- Separate Chaining
	- Array is a list of Linked Lists
	- When there's a conflict, just append to the linked list
	- Resize when load factor is anywhere from 1-3
	- Runtime: O(1 + lambda)
- Linear Probing
	- On a conflict, check the next location in the array, then the next, etc. until you find an open spot
	- Must use lazy deletion
	- Should resize when load factor is about 0.6
	- Cons: leads to clustering
	- Can result in a longer time for find
	- Resize when lambda = 0.5
- Quadratic Probing:
	- Formula for ith probe: H(key) + i^2 
	- Lazy deletion again
	- Secondary clustering (conflicts are resolved the same way)
	- Not guaranteed to find an empty spot 
	- Pros: Resolves the primary(?) clustering caused by linear probing
	- if lambda >= 1/2, quadratic probing will fail to find an open spot
	- Table size also must be prime 
- Double hashing
	- Formula for ith probe; h(key) + i * g(key)
	- g cannot output 0
	- No more secondary clustering, as each conflict is resolved differently
	- Always finds an empty spot only if the table size is prime and g(key) isn't a multiple of that prime number
	- Runtimes:
		- Unsuccessful Find: 1/(1 - lambda)
		- Successful Find: 1/(1 - lambda) ln (1/(1- lambda))
- Load factor: size / num buckets
	- Denoted using lambda
- Deletion should be done lazily for open addressing. For separate chaining you can just remove from the linked list
- Rehashing: pick another prime number to the be next number of buckets (or pick a power of 2 + 1). Then loop through all the elements and insert them again.