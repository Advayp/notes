- Data models affect how we think about the problem we're solving

## Relational vs. Document
- Main uses of relational
	- Transaction processing
	- Batch processing
- Relational was the defacto type of database for a while
- NoSQL: tried to compete with relational
- Causes of the emergence of NoSQL
	- Need for scalability
	- Need for FOSS 
	- Specialized query operations that are not well supported by the relational model
	- Need for a dynamic data model


## Object-Relational Mismatch
- Because of OOP, a translation layer is needed between application code and database models
	- ORM contribute to a solution to this problem
- JSON representation has better locality
	- Fetching relational info can lead to performing multiple queries or joins between tables and their related tables

## Many-to-One and Many-to-Many Relationships
- Normalization: Using something like an ID to store a reference to a string that can only have a strict set of values 
	- Less duplication
	- Easier to change (avoids write overheads)
	- Avoids ambiguity
	- Localization support
	- Better search
- Using something like this is better with relational databases, since joins for many-to-one or many-to-many relationships can be difficult for document models 
	- Document models also don't support joins very well
- If joins aren't supported, you'll end up having to make multiple queries 

## The Network Model
- A record could have multiple parents (unlike the hierarchical in which this quantity was limited to just one)
- Links between records were pointers
	- Pass through these links to access a record (access path)
- Main issue was that it was difficult to make changes to an application's data model

## The Relational Model
- Difference from network model: no access paths, everything is a tuple and can be easily accessed via some arbitrary query
- Query optimizer handles the "access path", so the developer doesn't have to worry about it like in the network model
- Comparison to document databases
	- Document databases are pretty much just like hierarchical models
	- But, for many-to-one and many-to-many relationships, they use document references and perform joins at read time

## Relational Versus Document Databases Today
- If the application has several one-to-many relationships, it's probably better to use a document model
	- Avoid shredding (splitting a document-like structure into multiple tables)
	- This just leads to more joins which are harder to perform anyway in a document model
- Requires an implicit access path
- Document model isn't great for extremely interconnected data
	- Relational is fine for this, but graph is probably the best
- Schema flexibility in the document model
	- Schema-on-read: Schema is only interpreted when reading from a database. This is similar to dynamic runtime type checking
	- Advantageous when:
		- Many different types of objects and it's not ideal to put each one of them in its own table
		- Structure of data is determined by external systems
		- 