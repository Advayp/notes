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
	- 

