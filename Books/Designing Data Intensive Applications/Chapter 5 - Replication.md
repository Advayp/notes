## Reasons to distribute data
- Scalability
- Fault tolerance/high availability
- Latency. For an application that's used globally, having local data centers would reduce latency and response times
- **Vertical Scaling**: Adding more resources to a system
- **Horizontal Scaling**: Each machine is a node, and communication between these nodes is managed by software. Simply scale by adding more nodes
- **Replication**: As the name implies, keep a copy of the same data on multiple nodes
	- Serves as a source of redundancy
- **Partitioning**: Divide a large dataset into smaller subsets called partitions. Each partition is assigned to a particular node (this is also called sharding)


**Some limitations**: Your machine must be able to hold the entire dataset. This works fine for smaller datasets, but becomes a problem for larger sets of data like those for Google.
- Difficulty in replication lies in how changes to data should be handled

## Leaders and Followers
- Each node that contains a copy of data is called a replica
- Leader-based replication: 
	- One of the replicas is designed the leader. All *write* requests are sent to the leader. Leader writes the data to its storage
	- Other replicas are called followers. When a leader writes a piece of data to its local database, it streams that change to the followers (this is called a replication log or change stream). Each follower takes this then updates its local copy appropriately
	- *Read* requests can be sent to either the leader or follower. *Write* requests must be sent to the leader
	- Databases and distributed message brokers use this usually

## Synchronous Versus Asynchronous Replication
- Question to consider: should replication happen sync or async?
- No guarantee of how long it takes to update a change, usually fast but again no guarantees 
- Advantages of Synchronous Replication
	- Follower always has a copy of data that's consistent with the leader
	- But, if the write fails, all other writes must be blocked
	- Can think of this as a blocking event on a thread
	- Any one node outage would cause the whole system to halt
- So, synchronous replication is pretty impractical. When enabled, usually we have one synchronous follower (and the others are async)
	- If this follower goes down, one of the async followers is made sync
	- This is called semi-sync replication

## Setting up New Followers
- Take a snapshot of the leader's database at some point in time. Goal is to do this without locking the database
- Copy the snapshot to the new follower node
- New follower requests all data changes that have happened since the snapshot was taken (usually found in a replication log)
- When the backlog changes have been processed, the follower has caught up, and can process changes as normal

## Handling Node Outages
- **Follower-Failure:** Can recover easily from a log of changes it's received from the leader. From this log, it can also determine the last applied change, and therefore the backlog of changes to apply.
- **Leader Failure: Failover.** One of the followers will have to be promoted to be the new leader, and clients need to be reconfigured to be sent to the new leader, and every follower must start consuming changes from the new leader. 
	- Choosing a new leader is usually done with an election process, but sometimes is directly appointed with a controller node.
	- In certain scenarios, two nodes could both believe they're the leader. This situation is called split-brain, and is dangerous because there's no way of dealing with conflicts. 
- **Declaring a Leader dead**: Usually based on a timeout, but sometimes can be manual too. Hard to find a good timeout since a large influx of requests can result in an increase in processing time.

## Implementation of Replication Logs
- **Statement-based replication**: Logs every write request that it executes and then sends that log statement to its followers.
	- The followers then parse and execute that statement.
	- For non-deterministic functions, we typically just send the direct value, like for things like `NOW()`.
	- Side effects are also things to watch out for, which can be non-deterministic.
- **Write-ahead log (WAL) shipping**:
	- Works similar to B-Trees and SSTables/LSM-Trees
	- Can use same strategy (but just distribute it) to replicate to followers
	- Log processing should be done such that it's deterministic. Reading a log should result in an exact copy of the same data structure found on the leader
	- Typically includes data changes at a very low level, and couples replication to the storage engine
	- Should consider an implementation that allows the follower to use a newer software version than the leader
- **Logical (row-based) log replication**:
	- Decouple replication log from the storage engine
	- Sends only changes in rows over, like so:
		- if the row was created, log contains the new values of all the columns
		- if a row was deleted, the log contains enough information to uniquely identify the row that was deleted (typically primary key)
		- if a row was updated, the log contains enough information to identify the row and the values of the updated columns.
- **Trigger-based replication**
	- Move replication up the application level instead of database level
	- Can be useful for handling conflicts
	- Trigger: lets you handle some custom logic that runs when a transaction completes. Logs to some external location, which then distributes to other systems
	- Pretty flexible, but harder to implement and more prone to bugs

## Problems with Replication Lag
- Alternate pattern for managing high volume of reads with not that many writes:
	- Have many followers, and distribute across those followers
- This is called read-scaling architecture
	- Works with async replication only, as sync is too blocking given the high volume of reads
	- Though, followers can fall behind at times, but will eventually catch up.
	- This is known as **eventual consistency**
- **Replication Lag**: How long it takes for a follower to reflect a leader's changes


### Reading Your Own Writes
- Writes are sent to leader, and followers take time to process writes. 
- So, after a write, a user may think that their data has been lost, which is problematic
- **Read-after-write consistency**: User's data is always immediately updated for *themselves*. No guarantee about other users immediately.
- How to implement
	- Read directly from the leader, after the write was performed. Need to predict what might've been modified by a user. 
	- If most things are editable, you can read from the leader for a certain period of time, or avoid reading from stale replicas by keeping track of replication lag

### Monotonic Reads
- When reading from two replicas subsequently with the second having more replication lag, it is possible for the user to see things happening backwards in time.
	- This is because the second replica is stale
- Implementing monotonic reads
	- Ensure users only read from one replica (by using a hash function)

### Consistent Prefix Reads
- Guarantees that writes made in a certain order are reader in the same order
- Common to sharded databases, because some partitions could be replicated slower than others

## Multi-Leader Replication
- Exactly what the name implies, more than one node can handle writes
- Introduced because single-leader replication leads to issues when the leader is down, and can be overloaded with a high volume of writes
- AKA master-master or active/active replication
- **Use cases**:
	- Multi-datacenter operation. Datacenters distributed across the world to be closer to users, each can have its own single-leader replication system. Writes are processed by closest datacenter and replicated async to other ones
- Main problem is conflict resolution. Same portion of data might be modified in two different data centers, need to have some way of resolving this conflict
- 