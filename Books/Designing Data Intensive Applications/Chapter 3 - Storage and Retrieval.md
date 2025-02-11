## Data Structures That Power Your Database
- Consider the example of only appending a key-value pair to a file
- Databases internally use a log (an append-only data file)
	- Log can include binary only data too
- The values of keys are found using indexes, which store some additional metadata 
	- Similar to a hash map
- Index is an additional structure that's derived from primary data. It's only introduced to improve the performance of queries
	- Writes are slower though than simply appending to the end of a file, since indices need to updated appropriately
- Databases don't introduce indices by default
	- This is left to the programmer since indices can be chosen to cater to the kind of queries the programmer needs for their application
- Hash Indices
	- Hash map mapping keys is stored in memory
		- All indices must fit into RAM though
- How To Avoid Running out of disk space (when the only write operation you do is append to a file)
	- Compaction: throw away duplicated keys, keeping the most recent version
	- Segment Merging: Combine compacted records into one, since compacting a record typically makes it smaller 
		- Done in the background while regular reads/writes are still being served
- Some other considerations for this model
	- **Deleting Records**: Append a special deletion record to the data file, which tells the merging process to discard any previous values for the deleted key
	- **Crash Recovery**: Store a snapshot on each segment's hash map on disk
	- **Concurrency Control**: Use only one writer thread
- Main problem with hash maps: Range queries are not efficient

## SSTables and LSM-Trees
- **Sorted String Table**: Store keys in sorted order 
- Merging segments is also pretty straightforward (it's like merging N sorted linked lists on Leetcode)
	- If multiple segments contain the same key, keep the value from the most recent segment and discard the values in older segments
- Can store less indices in memory, since the sorted order makes it easier to find the appropriate offset of a key
- Read requests often need to scan over several key-value pairs (since we're storing a smaller number of indices)

### Constructing and Maintaining SSTables
- Use a tree structure (red-black trees or AVL trees)
- Process
	- When a write comes in, add it to a balanced tree (stored in memory). This is called a memtable
	- After the tree exceeds some size, flush the contents to a SSTable file. This becomes the most recent segment of the database
	- When reading, search the memtable, and then each segment (most recent first)
	- Can write memtable to disk to handle crashes
- An SSTable uses an indexing structure called Log-Structured Merge Tree (LSM-Tree)
- Bloom filters are used to approximate the values present in the set of all keys, so that checking if a key is not present is faster

## B-Trees
- Most common type of index
- Standard index implementation of almost all relational databases
- Keep key-value pairs sorted by key
- B-trees break the database down into fixed-size blocks or pages
- Pages are referred to by others on disk. These page references are used to construct a tree of pages
	- One page is selected as the root of the B-tree
	- Each child is responsible for a continuous range of keys
	- This page consists of references and keys. The keys between the references indicate where the boundaries of those ranges lie. For example:
		- `ref_1 100 ref_2 200`
		- `ref_2` lies between keys with values of 100 and 200
- Leaf page: Page that contains no references

### Making B-Trees Reliable
- Use write-ahead logging (like databases) to recover from crashes
- Regarding concurrency control, latches (lightweight locks) are used 

### B-Tree Optimizations
- **Copy-on-Write:** modified pages are written to disk, and references are updated appropriately
- Abbreviate the key
- B-Trees try to lay out the tree so that leaf pages appear in sequential order. This is because page seeking via the references is extremely expensive.
- Add left/right pointers to enable more mobility throughout the tree structure
- Certain B-tree variants like fractal trees take inspiration from LSM Trees to reduce disk seeks

## B-Trees vs LSM-Trees
- LSM-Trees are faster for writes, B-Trees are faster for reads

### Advantages of LSM-Trees
- B-tree writes are slow for several reasons
	- Must write data twice, once to the WAL and once to the tree page itself
	- Overhead from writing an entire page at a time
- Write Amplification: One write to the database resulting in multiple writes to disk 
- LSM-Trees have a lower write amplification than B-trees, which makes them a better choice for write-heavy systems
- LSM-Trees are also compressed better

### Downsides of LSM-Trees
- The compaction process can increase request latency, because the finite resources of the disk might not be able to handle compaction and any incoming reads/writes
- At high-write throughput, it is possible the the compaction process won't be able to keep up with the rate of writes, creating more unmerged segments which can cause you to run out of disk space
- **An advantage of B-tree**
	- Each key is only stored in one spot, whereas in an LSM multiple copies of the same key could exist
	- Locks can be attached directly to the B-tree

## Other Indexing Structures
- Primary Key: uniquely identify a row in a relational table
- Secondary keys can also be used for performing more effective joins
- For tables with several secondary keys, the value corresponding to the key is typically just a reference to where that row is **(non-clustered index)**
	- Updating is fine with this model only if the size of the entry doesn't change, in which case the references need to be updated accordingly and the row might need to be moved into a new spot 
	- This dereference is sometimes too expensive, so sometimes the row is stored within the index itself **(clustered index)**
- **Covering index**: Like a clustered index, but only includes some of the columns of the row

### Multi-Column Indices
- **Concatenated index:** combine several fields into one index
- Useful if querying multiple columns at once is a common operation
- Two-dimensional indices can also be translated into a single number, which can then be used to construct a B-Tree
	- Usually a more specialized structure called an R-tree is used


### Full-text search and fuzzy indexes
- Fuzzy search: ignoring grammatical variations of words, searching for words within an edit distance, searching for words next to others

### Keeping everything in memory
- In-memory key-value stores are intended for caching use, where we don't care what happens to the data if power is lost
- Some in-memory databases write to disk for persistence, but serve read/write requests from memory
	- Main benefit is speed, but is significantly limited by size
- In-memory databases can support data structures that are hard to serialize to disk
	- Redis does this too, supporting priority queues and sets

## Transaction Processing or Analytics?
- Transaction: group of reads or writes that form a logical unit
- Data analytics has different access patterns: you need to scan over huge number of records and perform aggregations
	- This is called online analytic processing

## Data Warehousing
- Separate database that analysts can query as much as they want to
- Contains a read-only version of all the OLTP (online transaction processing) systems
- To get data from an OLTP system we:
	- Extract the data first
	- Transform it into an analytic-friendly schema
	- Load it into the warehouse
- Data warehouse advantages
	- Can be optimized for analytics
	- Reads don't interfere with any concurrent transactions on databases users indirectly write to
- Although data warehouses and OLTP systems look identical in terms of the kind of database structure they use, databases optimized for data warehousing expect a different kind of access pattern, and are optimized for that

## Stars and Snowflakes: Schemas for Analytics
- Star Schema (aka dimension modeling)
	- Fact table: represents an event that occurred at a particular time. Facts are captured as individual events. These get pretty large though
	- Some columns in the fact table are references to *dimension tables*, which each represent some particular quality of that event
- Variation called Snowflake
	- Dimension tables are further broken down 
- Tables can be very wide, as facts can encompass a variety of data
- Even dimensions and subdimension tables can be very wide, since these need to store a lot of metadata 
## Column Oriented Storage
- Data warehouse queries typically access multiple columns. In a database that uses row oriented storage, queries across multiple columns would end up loading all the other columns too in order to filter out those that don't match the query. This is pretty expensive.
- To fix this, data warehouses typically use column-oriented storage, where data is grouped by columns and not rows
- This can be encoded efficiently using one-hot encoding or run-length encoding if each column only takes on a specific set of values
- Note that you can also use different sort orders by sorting replicated data in a different way form the original
- Writing to column-oriented storage is done with an LSM tree. When a certain number of writes have accumulated, you write them in bulk to disk, merging with existing data


## Aggregation Data Cubes and Materialized Views
- **Materialized View:** Table-like object whose contents are the result of some query. Copy of the query results
	- When underlying data changes, materialized view must update too
- Data Cube (OLAP Cube): Grid of aggregates grouped by different dimensions
	- Aggregate some value (like price) based on some different qualities (e.g., product name and time)
- Main advantages: certain queries become extremely fast, since their results have been effectively precomputed 
- Main limitations: don't have the same flexibility as general queries
