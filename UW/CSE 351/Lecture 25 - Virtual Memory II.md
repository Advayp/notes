
## Paging
- Virtual address space > physical address space, so the virtual memory system must effectively make use of physical memory
- **Page**: another fixed-width unit of data transfer. $P = 2^p$ is the page size in bytes, with $p$ bits being used to identify each page
- Analogous to blocks and block size, but pages are much larger
- Physical memory and virtual memory are split into non-overlapping pages with different physical page numbers (PPNs) and virtual page numbers (VPNs)


## Virtual Memory and the Memory Hierarchy
- Physical memory can be thought of as a cache, holding the most recently and frequently used pages of data that are transferred to and from it. 
	- It's specifically a cache of the process' virtual address spaces, holds a subset of virtual pages, though most of these don't exist anywhere
	- It can also be thought of as a cache of a disk, transferring pages of data to and from the swap space and the disk is the larger, slower, cheaper level of storage "below"
- Physical memory cache parameters:
	- Large page size
	- Fully-associative
	- Write-back and write-allocate
	- Uses a sophisticated replacement algorithm determined by the OS


## Page Tables
- Address translation coverts a virtual address for a process into the corresponding physical address 
- This is done via a lookup tables called page tables 
	- key is the virtual page number (VPN)
	- value is the page table entry (PTE)
- Page table entry is similar to a cache line
	- Valid bit: whether or not this translation exists
	- Dirty bit: because physical-memory is write-back
	- Access rights bits

## Memory Protection

### Between Processes
- Goal is to make sure two processes don't interfere w each other's memory
- Handled via creating a page table for each process
- We make sure no page table entry contains the same PPN (to emphasize protection)
- Sharing is possible by having VPNs from different processes map to the same PPN

### Within a Process
- Use access right bits to prevent an individual process from misusing its own address space
- Read (R): is this process allowed to read the data on this page?
- Write (W): is this process allowed to change the data on this page?
- Execute (X): is this process allowed to use data on this page when fetching instructions from `%rip`?

[[Lecture 1 - Introduction, Binary]]
