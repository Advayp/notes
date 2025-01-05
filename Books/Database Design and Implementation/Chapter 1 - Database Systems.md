## Why a Database System?
- Database: collection of data, organized into records
- Requirements of a database system:
	- Persistence
	- Databases can be shared
	- Databases must be kept accurate
	- Databases can be very large
	- Databases must be usable

### Record Storage
- Common approach: store in files, one record per file
	- Too inefficient because large text files take too long to update and read

### Multi-user Access
- Concurrency is generally good, but can lead to race conditions in certain situations
- Concurrency must be limited 
- Any actions that conflict must be queued, and therefore cannot be concurrent
- Any undoable updates must only be seen by other users when they've been committed 

### Memory Management
- Databases must be stored in persistent memory
- Main conundrum: managing more data than memory systems, using slower devices, with multiple people fighting over access to data
	- Also must be recoverable and quick
- Caching is the main solution here

### Usability
- Users must be able to extract the data they want

## Database Engines
- Most database applications have a UI to interact with the database and an internal handler that updates the database based on a user's actions
- Latter is called the database engine
- Connection to UI can be embedded or server based
	- Embedded: runs in the same process as the UI code
	- Server-Based: executes on a dedicated server platform
- Server uses a scheduler to handle requests
- 