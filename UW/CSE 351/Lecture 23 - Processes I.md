
## Exceptions
- Transfer of execution/control to the kernel of the operating system in response to some event
- This invokes some kernel code called an event handler
- Three possible outcomes
	- Re-execute the instruction that cause the initial event - the event has been handled, but the original instructions did not complete properly
	- Execute the next instruction
	- Abort the process

## Types of Exceptions

### Asynchronous Exceptions
- Events external to the processor (aka interrupts)
- Always return control to the next instruction

### Synchronous Exceptions
- Caused by executing an instruction
- **Traps**: caused by instructions that intentionally transfer control to the operating system to perform some desired function. Return control to the next instruction
- **Faults**: Unintentional but possibly recoverable. If the fault is recoverable, the fault handler returns control to the current instruction (retry); if it's not, the fault handler will abort
- **Aborts**: Unintentional and unrecoverable. Only option here is to abort.

## Processes
- Instance of a running program/executable
- Provides processes with two key abstractions to maintain an interface between the process and the underlying hardware
- Logical control flow: Each process operates under the assumption that it has exclusive use of the CPU for executing its instructions
- Private address space: Each process believes it has its own section of memory

## Concurrency
- Important because your system runs 100s of processes at the same time 
- Two processes are said to run concurrently if their instruction executions overlap in time

## Context Switching
- Switching between processes is accomplished via context switching, which is managed by the operating system and exceptional control flow
- Pausing the currently-executing process:
	- Save current registers in memory
	- Schedule next process for execution
	- Load saved registers and switch address space


[[Lecture 1 - Introduction, Binary]]