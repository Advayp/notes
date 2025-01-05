
## Memory Hierarchy
![[Pasted image 20241103221549.png]]


## Block Size
- Machine-specific fixed unit of transfer between a cache and the storage level below
- Block Size (K) refers to this value, which is always a power of 2

## Cache Size
- Size of data the cache can store in bytes

## Memory and Blocks
- For a block size of K, every set of K will form a block. These blocks are labelled using numbers.
- To find the block number of an address $A$, compute $\text{floor}(\frac{A}{K})$. 
- $A\%K$ gives the block offset
- This information is actually encoded in the bits of an address
- Let $K = 2^{k}$
	- The block offset is the value of $k$ least significant bits of $A$
	- The block number if the value of the $m - k$ most significant bits


## Direct-Mapped Cache Placement
- To determine where to store a particular address, we do $\text{block number} \ \% \ \frac{C}{K}$
- This avoids the need for a replacement policy

[[Lecture 1 - Introduction, Binary]]