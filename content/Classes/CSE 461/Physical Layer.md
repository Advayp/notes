- How signals are used to translate to and from digital bits to analog signals

## Coding and Modulation
- Non-Return to Zero: high voltage represents a one, low voltage represents a zero
	- Clock recovery: receive needs frequent signal transitions to determine bit boundaries
- Return to Zero: high v is a 1, low v is a 0, then go back to 0V for a reset
	- Wastes half the slots
- 4B/5B: Map every 4 bits to 5 bits without long runs of zeroes
	- has at most 3 zeroes in a row
	- Invert signal level on a 1 to break up long runs of 1s

## Passband Modulation
- Can transmit bits by shifting amplitude, frequency, and phase 
	- Change all at the same time to get the highest bitrate 

## Link Model
- Rate in bits/second
- Delay in seconds, related to the length
- L = M/R + D
	- L = latency
	- M = number of bits to send
	- R = rate in bits per second
	- D = delay in seconds

## Message Latency
- First bit on wire -> the final bit arriving at destination
- Transmission Delay
	- M bits / R bits/sec
- Propagation Delay
	- Length / speed of signals