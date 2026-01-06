- Functions that you can pause/resume
- Active coroutine must purposely yield before switching to another coroutine, no interruptions
	- will run uninterrupted until it gets blocked or voluntarily yields

## API
- yield
	- pause current coroutine
- spawn
	- create a new coroutine
- join
	- wait for a coroutine to finish