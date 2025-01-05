
## Cache Access
![[Pasted image 20241105203730.png]]
- $k = log_2 (K)$
- $s = log_2(\frac{C}{K})$
- $t = m  - s - k$
- $m$: Address width

## Associativity
- **Set Associative Cache**: Allow each block to fit into a specified set of locations
	- An E-way set associative cache uses sets of size E
- Number of sets is given by: $S = \frac{\frac{C}{K}}{E}$


## Cache State
- In an uninitialized cache, there's always some form of garbage data 
- For this reason, caches include a valid bit along with other management bits along with each block.
- The combination of all of these things is called a cache line

## Cache Misses
- Compulsory Miss: if we access a cache for the first time, we're guaranteed to have a miss
	- Reduced by a larger block size
- Conflict Miss: if more references map to the same set than our associativity allow to coexist, this causes misses when we revisit the earlier references.
	- Reduced by higher associativity
- Capacity Miss: If total amount of data > cache size, we don't have the capacity to store everything
	- Reduced by a larger cache size
	
[[Lecture 1 - Introduction, Binary]]