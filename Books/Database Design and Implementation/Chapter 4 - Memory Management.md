## Two Principles of DB Memory Management
- **Principle 1**: Minimize Disk accesses. Use caching in memory.
- **Principle 2**: Don't rely on virtual memory. 
	- Operating system's page swapping strategy can impair the database engine's ability to recover from a crash
	- Operating system has no idea which pages are in use by the DB and which pages the database engine doesn't care about anymore
- DB engine must manage its own pages.
	- Allocate a small number of pages known to fit in physical memory (known as buffer pool)
	- The engine then manages writing to and reading from pages


## Managing Log Information
 - Changes to database must be tracked in logs, so that they can be undone
 - Logs are stored in log records
 - Log Manager is responsible for writing log records to the log file, not reading or processing them
 - Logs can have varying size
 - Algorithm to write logs
	 - Allocate one memory page, denoted P, to hold the contents of the last block of the log file 
	 - When a new log record is submitted:
		 - Append the new log record to P if P has room
		 - If not, write P to disk and clear its contents

###  Buffer Manager
- Responsible for the pages that hold user data 
- Allocates a fixed set of pages, called the buffer pool
- Terminology:
	- A page is pinned i f some client is currently pinning it, otherwise it's unpinned
- Buffer manager is obligated to keep a page available to its clients for as long as it is pinned.
	- Once a page becomes unpinned, the buffer manager is allowed to assign it to another block
- Four possibilities can occur when a client asks to pin a page to a block
	- The contents of the block is in some page in the buffer and
		- Page is pinned
		- Page is unpinned
	- The contents of the block is not currently in any buffer and
		- There exists at least one unpinned page in the buffer pool
		- All pages in the buffer pool are pinned

### Buffers
- Buffer is the object that contains metadata regarding a particular page in the buffer pool, like whether it's pinned or not
- Only two reasons a buffer will write a modified page to disk:
	- Page is being replaced because the buffer is getting pinned to a different block
	- Or the recovery manager needs to write its contents to disk to guard against system crashes

### Buffer Replacement Strategies
- When more than one buffer page is unpinned, the buffer manager must decide which page to replace
- Naive: Remove the first unpinned page found
- FIFO: Choose the buffer that was least recently *replaced*
- LRU: Choose the buffer that was least recently *used*
- Clock: Chooses the first unpinned page it finds, but starts it scan at the page after the previous replacement (Like next-fit in malloc)
