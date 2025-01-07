## Designing a Record Manager
- Several questions:
	- Should each record be placed entirely within one block?
	- Should all records in a file be from the same table
	- Is each field representable using a fixed number of bytes
	- Where should each field value be positioned within its record

### Spanned vs. Unspanned Records
- Spanned record: a record can be stored over multiple files
- Record manager decides whether or not to create a spanned record 
- If records can be larger than a block, spanning is necessary
- Main disadvantage is that spanning records create more complexity regarding data access

### Homogeneous vs. Non-homogeneous Files
- File is homogeneous if all records come from the same table
- Single-table queries are easier with homogenous files, but multiple-table queries become difficult
- Putting related data from different tables in the same file is a technique known as clustering

### Fixed-length Versus Variable-Length Fields
- Fixed length is used when possible
- Variable length results in issues when modifying, as the field could get larger and as a result the record manager might need to move other records in the file around
- Strings are stored in three different ways:
	- variable-length representation in which the record manager allocates the exact of space the string requires
	- reference to string is stored
	- same size is allocated for each string

### Placing Fields in Records
- Alignment can cause problems regarding field ordering, and use the least amount of padding necessary
- External fragmentation is also something to consider here

