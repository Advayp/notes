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
- Data locality for queries
	- Documents are stored as encoded, continuous strings
	- Accessing one part of a document accesses the whole portion, which is good spatial locality
		- This is also a disadvantage though if you're dealing with large documents that aren't frequently referenced
	- Data stored in relational tables can be stored across multiple tables which requires multiple index look-ups
	- Updates to documents require the entire document to be rewritten if the size of the document increases
		- Some good practices: Keep documents small, avoid writes that increase size significantly

## Query Languages for Data
- SQL is declarative solution to the query language problem, which was previously handled through imperative syntax
- SQL follows relational algebra pretty closely
- Imperative languages specify that code must be run in a particular order, which has issues regarding the following:
	- Implementation detail is present in the code itself, which means that performance optimizations on behalf of the database will have to change the code itself
	- It's harder to parallelize imperative languages due to the "order" constraint

## MapReduce Querying
- Model for processing large amounts of data in bulk across many machines
- Typically used for performing read-only queries across many documents
- In MongoDB,
	- Map over all objects, emitting some key-value pair for each
	- The reduce function is called on all the values that have the same key
- Note: map and reduce must be pure functions

## Graph-Like Data Models
- Handle many-to-many relationships pretty well
- Two components:
	- Vertices (aka nodes or entities)
	- Edges (aka relationships or arcs)

## Property Graphs
- Vertex:
	- Unique ID
	- Set of outgoing edges
	- Set of incoming edges
	- A collection of properties (key-value pairs)
- Edges:
	- ID
	- Start vertex
	- End vertex
	- Label to describe relationship
	- A collection of properties
- Can think of these as two relational tables, one for the vertices and one for the edges
- Some notable aspects
	- Can connect any edge to any vertex, no schema restrictions here
	- Can traverse the graph from any vertex
	- Can store several kinds of information in a single graph

### Querying Graph DBs
- Programming language called Cypher is often used, but can do with regular SQL as well
- SQL is possible, but you need to know joins in advance
- In SQL, you need recursive common table expressions to implement this properly
	- Though, in SQL, this requires a lot more lines to write properly

## Triple Stores and SPARQL
- Triple Store model is similar to the graph model, with different terminology
- All information is stored in the form (subject, predicate, object)
- Subject is equivalent to a vertex in a graph
- Object is either:
	- Another vertex, which means the predicate is an edge
	- A primitive value, which means the predicate is a property on the vertex

### The semantic web
- Websites publish text and pictures for humans to read, so why don't they also publish information as machine-readable data for computers to read
- Didn't really go anywhere, but still lead to some useful discoveries

### The RDF Data Model
- A mechanism for different websites to publish data in a consistent format, which is then accumulated into a database of "everything"
- RDF is pretty similar to a triple-store model, but each of the constituents is a URI

### SPARQL
- Query language for triple-stores using the RDF model
- Can use same syntax for properties and edges since predicates in a triple-store model can double as properties and edges

## Datalog
- Foundation of most query languages
- Similar to a triple-store model, except data is return as `predicate(subject, object)`
- Requires a different way of thinking about data, but can be useful if the data is extremely complex

