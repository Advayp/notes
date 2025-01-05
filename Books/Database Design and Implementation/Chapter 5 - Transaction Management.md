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