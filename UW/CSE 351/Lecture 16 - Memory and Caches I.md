## IEC Prefixes
![[Pasted image 20241027134745.png]]
![[Pasted image 20241027134759.png]]
- `X` is the number of powers of $2^{10}$
	- E.g.,: $2^{30 + 2}$ = $2^{2} \cdot (2^{10})^{3}$ = 4 Gibi Bits


## Cache and Cache Mechanics
- Caches are introduces because accessing memory is very slow. 
- Caches are usually abbreviated with the `$` symbol
- Data is transferred between caches and memory in blocks, which are fixed units of transfer specified by the machine (much larger than a word)
- When accessing memory, CPU always checks the caches first
	- If it's found, this is a **cache hit**, and the data is returned quickly
	- If it's not found, this is called a **cache miss**, and the data is fetched from memory and copied into the cache

## Principle Of Locality
 - Temporal locality: recently referenced items are likely to be referenced again in the near future
 - Spatial Locality: items with nearby addresses tend to be referenced close together in time

## Cache Performance Metrics
- **Hit Time**: how long a cache hit takes, the time to check the cache and return data to the CPU. Based on hardware
- **Miss Penalty**: How long it takes to fetch a block of data from memory. This parameter is based on the cache and memory hardware
- **Hit Rate/Miss Rate**: The fraction of your code's memory access that result in a cache hit/miss. HR + MR = 100% by definition. This is based on your code
$$
\text{AMAT} = \text{Hit Time} + \text{Miss Rate} \cdot \text{Miss Penalty}
$$
- AMAT: Average Memory Access Time

[[Lecture 1 - Introduction, Binary]]