- A blocking syscall from one coroutine blocks the entire OS-thread that coroutine is running on
- Coroutines also have to keep track of their stack, which must stay allocated the entire time a coroutine is suspended. This is quite expensive.


## Designing a Stackless Coroutine
- Can use something similar to a state machine, each .await is a transition edge between states in the state machine
- Each state only stores the live variables at that point
- To handle blocking functions, we can give each coroutine a run method that returns either Ready(T), meaning that the blocking call has finished with some value, or Pending, which means the coroutine is still blocked
	- This adds a few states to the state machine, but the run method allows the coroutine to make progress
- Scheduler runs on each core, which means memory usage is tied to the number of cores and not the number of coroutines

## Waker
- Use waker to arrange resumption in the future
- Relinquish CPU to the operating system during I/O tasks
- After I/O tasks, wake the coroutine up and put it in the queue again

## Future vs. Task
- Future: passive state machine, via .await
- Task: Futures compose together to make a task. A task is a future the executor owns and polls
	- expose parallelism via tasks

- join!: run multiple futures concurrently, wait for all to complete
- select!: run multiple futures concurrently, take the first to complete
