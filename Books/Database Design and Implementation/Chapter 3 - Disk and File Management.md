## Persistent Data Storage

### Disk Drives
- Comprised of one or more rotating platters, which themselves consist of tracks that hold sequences of bytes
- An arm reads and writes data to each track
- Performance is based on four things:
	- Capacity: Number of bytes that can be stored
	- Rotation speed: rate at which the platters spin, usually given in revolutions per minute
	- Transfer rate:  Speed at which bytes pass by the disk head to be transferred to/from memory
	- Seek time: Time it takes for the actuator (the arm) to move the disk head from its current location to the requested track. Usually an average is calculated to get an understanding of overall performance

### Accessing a Disk Drive
- **Disk access**: request to read bytes contiguous on a track from the disk or write bytes to it
	- Step 1: Seek to the specified track
	- Step 2: Wait for the platter to rotate until the first byte is positioned at the head (called rotation delay)
	- Step 3: Read/write the data (transfer time)

### Improving Disk Access Time
- **Disk Caches**: Disk is accessed in sectors. Disk caches hold sectors that have recently been accessed. These are big enough to hold thousands of sectors
	- Pre-fetches the whole track a sector is contained within for spatial locality
- **Cylinders**: Databases can minimize the number of disk accesses by storing related information in nearby sectors. 
	- E.g. for files occupying more than one track, it's best to store that file on the same track of other platters, minimizing seek time
	- Set of tracks having the same track number is called a cylinder
- **Disk Striping**
	- Use multiple disk drives to leverage multiple actuators, enabling responses to multiple sectors simultaneously
	- Load management is key here, as if some of the added disks aren't used it's a waste
	- Disk striping involves giving the operating system the illusion of a big disk, containing as many sectors as all the disks combined. This effectively distributes the database equally among the various small disks.
![[Pasted image 20241226201647.png]]

### Improving Disk Reliability by Mirroring
- Keep two identical versions of the disk, mirroring changes in one to the other
- Done using a special controller
- Mirrors must be updated sequentially. If done in parallel, issues in writing to one can cause both processes to fail

### Improving Disk Reliability by Storing Parity
- Mirroring is problematic because it requires double the number of disks to store the same amount of data
- Parity has one key property: the value of any bit can be determined from the other bits if the parity is also known
- In practice, we use a parity disk.
	- Each bit of the parity disk is found by taking the parity of all the corresponding bits in the other disks used  for disk striping
- Drawbacks
	- More time-consuming, because a requires both a write and a read
	- The failure of one disk is costly to handle, since all the other disks are required to construct its data


### RAID
- Strategies mentioned above are part of a larger collection called RAID, or Redundant Array of Inexpensive Disks.
- RAID has seven levels
	- RAID-0 is striping
	- RAID-1 is mirrored striping
	- RAID-2 uses bit striping and a redundancy mechanism based on error-correcting codes instead of parity. Has poor performance and is difficult to implement
	- RAID-3 and RAID-4 use striping (byte striping for RAID 3 and sector striping for RAID-4) and parity
	- RAID-5: Similar to RAID-4, but parity information is stored on every disk instead of a dedicated, parity disk
	- RAID-6: Like RAID-5, but keeps two kinds of parity information 
- RAID-1 and RAID-5 are the most popular

### Flash Drives
- Disk drives' main issue is its reliance on mechanics for accessing data, which is much slower than relying on electronics, like RAM
- Flash drives use semiconductor tech which is like RAM but doesn't require a power supply
- Although flash drives are much faster, flash memory can wear out (though this isn't as a big an issue in modern times)
- Main issue for mass adoption is the price, which is significantly more than that of a disk drive
- Flash memory can be used a sort of initial storage for the data in a database. Any overflows will go straight to the disk

## The Block-Level Interface to the Disk
- Just like blocks in CSE 351
- OS usually provides the following interface for interacting with blocks:
	- `readblock(block_number, page_number)`
	- `writeblock(block_number, page_number)`
	- `allocate(payload_size, n)`: Finds a payload of `payload_size` as close to the block with block number n
	- `deallocate(size, n)`: Deallocates `size` bytes starting at block `n`
- Two main ways of keeping track of free blocks
	- Disk map: bit map storing information about whether or not a particular block is allocated
	- Free list: chain of chunks, where each chunk is a contiguous sequence of unallocated blocks
	- Similar to an explicit free list that's used to implement `malloc` and `free`

## The File-Level Interface to the Disk
- Java has a class called `RandomAccessFile`, which provides an API for the file system
- This type of interface enables a file to be considered a series of blocks
- When seeking to a particular byte in a file, the following happens:
	- Byte position -> logical block reference
	- Logical block reference -> Physical block reference
		- Harder and depends on what's called a file system directory (a mapping of logical block references to physical block references)
		- Three strategies:
			-  Contiguous Allocation: store each file as a sequence of contiguous blocks
			- Extent-based allocation: stores each file as a series of extents, which themselves are series of blocks
			- Indexed allocation: Linked list of blocks in a sense

## Database System and the OS
- Block-level interface
	- More granular control over disk access
	- Not constrained by OS limits on files - more versatility with regard to the structure of the db
	- But, it's a lot harder to implement
- File level interfaces are impractical as their subjection to OS requirements is not compatible with the requirements of a database
- A compromise is storing data in one or more OS files and treating each file as a raw disk

