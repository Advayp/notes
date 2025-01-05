## Transactions
- To prevent data loss or corruption, databases force client programs to consist of transactions, which are groups of operations that behave as a single operation
- This notion of being a single operation is defined by four main properties:
	- **Atomicity**: All or nothing. Either all the operations succeed (commit) or all of the constituent operations fail (transaction does a rollback)
	- **Consistency**: Every transaction is pure. It can be executed independently of other transactions
	- **Isolation**: Each transaction behaves as if it's the only thread using the engine. In the case where multiple are running at the same time, result should be the same as if they were executed in order in a series
	- **Durability**: Changes made by a committed transaction are guaranteed to be permanent
- Transactions hide the buffer manager from the client so the buffer manager can  make calls to the concurrency and recovery managers

## Recovery Management
- Reads and processes the log
- Three functions: write logs, rollback transactions, and recover the database after a system crash

### Log Records
- Writes log records to manage information about transactions
- Four kinds of log records: start records, commit records, rollback records, and update records
	- Start record is generated when a transaction beings
	- Commit or rollback is written when a transaction terminates
	- Update is written when a transaction modifies a value
- Multiple transactions are written to the log concurrently

### Rollback
- Find the update log records tied to a given transaction and restore the original contents of each modified value
- Read log file from back to front because of temporal locality

### Recovery
- Recovery is performed each time the database engine starts up
- Goal is get the database to a state where:
	- All uncompleted transactions should be rolled back
	- All committed transactions should have their modifications persisted
- Algorithm for recovery during a crash
	- Undo stage (undoing modifications of incomplete transactions)
		- If the current log record is a commit record, add that transaction to the list of committed transactions
		- If the current record is a rollback record, add that transaction to the list of rolled-back transactions
		- If the current record is an update record not on the commit or rollback list, restore the old value 
	- Redo stage (persisting committed transactions)
		- If update record and on the commit list, restore new value

### Undo-only and Redo-only recovery
- Undo-only recovery
	- Force buffers to disk before writing the commit record to the log
- Redo-only recovery
	- Ensures buffers stay pinned until a transaction is committed 
	- Faster than undo-redo recovery, though uses up more buffer baggage

### Write-Ahead Logging
- Write update logs before the modified buffer page
- This prevents cases where the buffer page is written to disk without the update log
	- Which means that recovery is not possible since there's no associated log

### Quiescent Checkpointing
- When dealing with large log files, parsing through them for recovery can be expensive
- Checkpointing takes advantage of the fact that the recovery algorithm can stop searching the log as soon as it knows the following:
	- All earlier log records were written by completed transactions
	- The buffers for those transactions have been flushed to disk
- Quiescent checkpoint:
	- Stop accepting new transactions
	- Wait for existing transactions to finish
	- Flush all modified buffers
	- Append a quiescent checkpoint record to the log and flush it to disk
	- Start accepting new transactions
- Usually written during start-up

### Non-quiescent Checkpointing
- Instead of waiting for all transactions to stop, note which ones are running when the checkpoint is made
- When the recovery manager reaches this, it can determine if it should continue going through the log record

### Data Item Granularity
- Unit of logging is called a recovery data item
- Size of a data item is called its granularity

## Concurrency Manager
- Responsible for the correct execution of concurrent transactions

### Serializable Schedules
- History of a transaction is the series of database actions made by that transaction
	- Database action: read or write of a disk block
- When multiple transactions are running concurrently, the database engine interleaves their execution, which is called a schedule
- Serial Schedule: transactions run back-to-back and are not interleaved
- Non-serial schedule is serializable if it produces the same result as some serial schedule
	- Serial schedules are correct, so serializable schedules must also be correct
- A schedule is correct if and only if it is serializable 

### The Lock Table
- Locking can postpone the execution of a transaction to ensure serializability 
- Every block has two kinds of lock
	- Shared lock: Other transactions are only allowed to have shared locks on it
	- Exclusive lock: No other transaction is allowed to have any kind of lock on it
- Lock table: database engine component responsible for granting locks to transactions
- Transactions don't explicitly lock or unlock blocks
	- Getting obtains a shared lock
	- Setting obtains an exclusive lock
	- Commit unlocks all its locks
- Locks ensure that transactions are serializable 

### Serializability Problem
- Once a transaction unblocks a block, it can no longer lock another block without impacting serializability 
	- This is because in between the unlock and lock another transaction can commit, which means that these two transactions aren't serializable
- To solve this, we use two-phase locking
	- 1st phase: acquiring all necessary locks
	- 2nd phase: releasing all acquired locks

### Deadlock
- When there's a cycle in the wait-for graph, the graph that shows which transactions a particular transaction is waiting on 
- When dealing with a deadlock, you can rollback the transaction whose lock request caused the cycle
- In certain situations though, deadlock may occur with an acyclic waits-for graph
- Detecting a cycle is also expensive
- Simpler strategies exist, but have an increasing number of 


### File-level Conflicts and Phantoms
- At the file-level, the methods `size` and `append` also conflict
- Problem with two transactions (T1 which appends, T2 which reads size):
	- T2 will need to obtain an slock on blocks that don't exist yet, since T1 hasn't appended them
	- This is fixed by allowing transactions to lock the end-of-file marker (xlock for append, slock for size)

### Multiversion Locking
- Conflicts can occur between read and update transactions
- This works by storing multiple version of each block
	- Each version of a block contains a timestamp with the last commit time of  a transaction
	- When a read-only transaction requests a value from a block, the concurrency manager uses the version of the block that was most recently committed
- Multiversion locking ensures that read-only transactions do not need to obtain locks and never have to wait

### Data Item Granularity
- Unit of locking is called a concurrency data item
- Principles of concurrency aren't affected by the granularity of the data item used
- Smaller granularity enables more concurrency, but also requires more locks
- Data record granularity:
	- Handled by the record manager
	- Main problem is with phantoms, since data records can get inserted into existing blocks
