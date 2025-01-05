
## Page Hit
- Page hit occurs if the request page currently lives in physical memory
- Process
	- CPU sends a virtual address to the memory management unit (MMU)
	- MMU uses the virtual address' page number and the value in the page table base register to lookup the PTE in the page table
	- Request PTE is returned to the MMU (valid bit must be 1)
	- MMU translates virtual address to a physical address and uses the physical address to request the desired data from memory
	- Cache/memory returns the requested data to the CPU

## Page Fault
- Happens when the requested page is not currently in physical memory (currently on the swap space in the disk)
- Process
	- CPU sends a virtual address to MMU
	- MMU uses the VPN and the value in the PTBR to get the PTE
	- Requested PTE is returned to the MMU (valid bit must be 0)
	- MMU triggers a page fault exception
	- Page fault handler identifies a victim page from physical memory
	- Handler pages in the requested page and updates the corresponding PTE
	- Handler returns control to the process, which restarts the faulting instruction for a guaranteed page hit

## Translation Lookaside Buffer
- Reduces number of memory accesses needed during address translation
- To access this, we split the VPN into a TLB Index field based on how many sets are in the TLB and then a TLB Tag 


[[Lecture 1 - Introduction, Binary]]