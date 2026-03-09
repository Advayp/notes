## Delivery Models
- Unicast: single source -> single destination
- Broadcast: single source -> multiple destinations (all other nodes in the network)
- Multicast: single source -> multiple destinations (subset)
- Anycast: any subset of nodes -> any subset of nodes

## Goals of Routing Algorithms
- Correctness
- Efficient paths
- Fair paths
- Fast convergence
- Scalability

## Rules
- Decentralized
- All nodes are alike
- nodes can only communicate with their neighbors
- Nodes operate concurrently
- Nodes/links/messages can fail

## Shortest Path
- Approximate best by a cost function that captures the factors
- Assign each link a cost
- Define best path between each pair of nodes as the path that has the lowest total cost
- Pick randomly to break any ties
- Optimality Property
	- Subpaths of shortest paths are also shortest paths
- Routing table only needs to store the next hop node because of this

## Sink Trees
- For a destination, a sink tree is the union of all shortest paths towards the destination
	- similarly a source tree


## Distance Vector Routing
- distributed version of Bellman-Ford
- Slow convergence though
- Each node maintains a vector of distances and next hops to all destinations
	- Initialize vector with 0 cost to self and infinity to other destinations
	- Periodically send vector to neighbors
	- Update vector for each destination by selecting the shortest distance heard after adding cost of neighbor link (using the best neighbor for forwarding)


## Link-State Routing
- Flood the network topology 
- Each node computes its own forwarding table


## DV/LS Comparison
- Main difference is in convergence and scalability. Link-state converges quickly but doesn't scale as well as DV


## BGP Routing
- Paths between autonomous systems must have each of the middle nodes in the path making money. AS's make money when one of their customers is in the path as well.
- Prefer customer paths over p2p paths, as customer paths make money. Prefer p2p over provider paths, as provider paths lose money.
- Out of customer paths, pick the ones with the shortest number of AS hops
- AS i only advertises one path to AS j
	- If the selected path is a customer path, you can advertise to customers, peers, and providers, since you'll be making money
	- If the selected path is a peer path, you can advertise to customers 
	- If the selected path is a provider path, only advertise to customers