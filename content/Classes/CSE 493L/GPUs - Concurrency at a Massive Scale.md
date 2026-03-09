- Originally used only for graphics, hard to use for things other than graphics
- Some people found that you can do linear algebra on GPUs, and it's pretty fast

## Architecture Overview
- CPU initiates computation on the GPU
- Discrete GPUs have their own dedicated memory
- Integrated GPUs often share w/ host CPU

## Single-Instruction, Single-Data
- one instruction operates on a single piece of data

## Multiple-instruction, multiple-data
- Multiple cores executing instructions that could be on different pieces of data
- All processors connected via globally available memory

## Single-Instruction, Multiple-Data
- A multiprocessor machine that executes the same instruction on all the processors
- But it operates on different data streams


In GPUs, the programming model is SIMT, or single instruction multiple threads. All threads share the same program. Developers can write scalar programs which are executed on the vector hardware.

GPU kernels are composed of thousands of threads.

## Memory System
- Divide memory into local and global sections
- No cross-thread memory

Can coalesce memory accesses by interleaving memory accesses

