
## Cache Writes and Data Consistency
- **Write-Hit**: Writing data when it's already present in the cache
	- A **write-through** cache writes the change into the block in the cache and in the level below
	- A **write-back** cache writes the change only into the block in the cache, but notes that this block has been updated
- **Write-Miss**: Writing data when it's not present in the cache
	- A **write allocate** cache will load the requested block into the cache before executing a write-hit
	- A **no-write allocate** cache skips the cache and sends the write directly to the level below
[[Lecture 1 - Introduction, Binary]]