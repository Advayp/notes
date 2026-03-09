- Provides end-to-end connectivity across the network
- UDP: unreliable messages (message boundaries preserved)
- TCP: reliable stream
- TCP has connections, bytes are delivered once, reliably, and in-order
	- TCP also has arbitrary length content, whereas UDP doesn't
	- TCP has flow control to match sender/receiver, along with congestion control


## UDP
- used by apps that dont want reliability/byte-streams
- no checksum, glorified IP


## TCP
- 3 phases
	- connection establishment
	- sliding windows/flow control
	- connection release
- conn. est.
	- agree on parameters like the maximum segment size
	- three way handshake
	- client syn (seq = x)
	- server syn (seq = y, ack = x + 1)
	- client (seq = x + 1, ack = y + 1)
	- syns messages are retransmitted if lost
- conn. release
	- use a symmetric close where both sides shutdown independently
	- active party sends a fin message, which is then acked. passive party finishes transmitting whatever data it has left, and then sends a fin message which is then acked by the active party.

## Sliding Window
- Various implementations
- Go back N
	- sender
		- LFS: last frame sent
		- LAR: last ack rec'd
		- send while LFS - LAR < window size
		- window advances only when LAR advances to the next sequence number
	- receiver
		- receiver keeps only a single packet buffer for the next segment
		- maintain LAS, last ack sent
		- when the next received packet has a seq number of las + 1, ack it. If not, drop it
- selective repeat
	- buffer out-of-order segments
	- ACK conveys highest in-order segment, plus hints about the out-of-order segments

## ACK Clocking
- helps run with low levels and loss and delay
- Network smooths out the burst of data segments, ack clock transfers smooth timing to sender


## Adaptive Timeout
- Estimates mean and variance with a moving average
- sets timeout to the mean + 4 times the variance

## Congestion
- traffic jam in network
- queues help absorb bursts, but if the input rate is greater than the output rate you have congestion
- having an infinite queue doesn't help because that increases queue time, which in turn increases latency


## TCP Tahoe/Reno
- Bandwidth allocation
	- efficient: means most capacity is used but no congestion
	- fair: every sender gets a reasonable share of the network

## Fair Allocations
- Cant always have efficiency and fairness
- Focus on avoiding starvation, i.e., a node that cannot use any bandwidth
- bottleneck for a flow of traffic is the link that limits its bandwidth, different flows can have different bottlenecks

## Max-Min Fairness
- Flows bottlenecked on a link get an equal share of that link
- Max-min fair allocation is one that
	- increasing the rate of one flow will decrease the rate of a smaller flow
- goal is to maximize the minimum flow
- steps
	- start with all flows at rate 0
	- increase the flows until there is a new bottleneck in the network
	- hold fixed the rate of the flows are bottlenecked
	- go to step 2 for any remaining flows

## Bandwidth Allocation Models
- Open loop vs closed loop
	- Open: reserve bandwidth before use
	- Closed: use feedback to adjust rates
- Host vs networking support:
	- who sets/enforces allocations
- Window versus rate based
- TCP is closed loop, host driven, and window-based

Additive Increase Multiplicative Decrease
- Control low hosts can use to reach a good allocation
	- additively increase rate while network not congested
	- multiplicatively decrease rate when congested
- requires only binary feedback from the network
- feedback signals
	- packet lose
		- hard to get wrong
		- hear about it late
	- packet delay
		- hear early, but need to infer congestion
	- router indication
		- hear about congestion early, but requires router support

Slow-start
- double congestion window every RTT

## TCP Tahoe
- Initial slow-start phase
	- cwnd += 1 packet per ack
- later additive increase
	- cwnd += 1/cwnd packets per ack
	- roughly adds one packet per RTT
- switch to AI when cwnd > ssthresh
	- set ssthresh = cwnd / 2 after loss
	- begin with slow start after timeout
		- do this to recover the ack clock
- ack clock is important because you get an idea of what's happening in the network
	- timeouts pause acks, which deteriorates the ack clock


## Fast Recovery
- TCP uses cumulative acks, which carry the highest in-order seq number
- Duplicate acks tell us that new data did arrive, but it wasn't the next segment
	- which means the next segment may be lost
- treat three duplicate acks as a loss
	- retransmit next expected segment, even before the timeout occurs
	- some repetition allows for reordering, but still detects loss quickly

## Network-Side Congestion Control
- Router indicates that congestion is happening
	- called explicit congestion notification
	- requires router support, so this only really works within data centers where you can control all the routers
- Router detects onset of congestion via its queue
	- mark affected packets in the IP header
- marked packets arrive at receiver, treated as loss
- TCP receiver reliably informs TCP sender of congestion
- pros
	- congestion detected early, no loss
	- no extra packets need to be sent
- cons
	- need router/host support
	- more work at routers
- 

