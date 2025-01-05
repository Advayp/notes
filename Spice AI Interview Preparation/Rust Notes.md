- Type conversions must be explicit using the `as` keyword
- Three types of memory in Rust
	- data memory: fixed in size and static.
	- Stack memory: declared as variables within a function. Location of this memory never changes, so stack data is very fast to access
	- Heap memory:  Data created while the application is running
- Enum elements can have one more data types
	- See https://tourofrust.com/30_en.html
- The `Option` enum represents nullable values
- The `Result` enum allows us to return a value that has the possibility of failing 
- Use `?` when dealing with results to automatically handle errors
	- See https://tourofrust.com/38_en.html
- `.unwrap()`: Can use on options or results to get the value contained within the `Some` or `Ok`.
	- Panics if the function returned `None` or `Err`
- Create vectors with `vec![]`
	- Iterate through using `iter()`
	- See https://tourofrust.com/40_en.html


## Ownership and Borrowing:
- **Binding** a type to a variable name creates a memory resources that the rust compiler will validate through its whole **lifetime**. The bound variable is called the **owner**
- End of scope deallocates and deconstructs the resources in that scope
	- This deallocation/deconstruction is called a drop
- Dropping is hierarchical
	- For a struct, the struct itself is dropped, and then its children are dropped individually
- Memory resources can only be dropped once
- When an owner is passed as an argument to the function, ownership is moved the function parameter
	- After the move, the variable in the original function cannot be used
	- During a move, the stack memory of the owners' value is coped to the function call's parameter stack memory
- Ownership can also be moved out from a function, like during a return
- Can borrow access to a resource using `&`
	- If the original resource is moved though, the compiler raises an error
- We can borrow mutable access to a resource using the `&mut` operator
	- A resource owner cannot be moved or modified while mutably borrowed
	- See https://tourofrust.com/49_en.html
	- When using mutable references, you can set the owner's value using the `*` operator. See https://tourofrust.com/50_en.html
- Passing around borrowed data
	- Rust only allows one mutable reference or multiple non-mutable references but not both
	- A reference must never live longer than its owner
- Explicit lifetimes
	- Functions can be explicit by parameterizing the function signature with symbols that help identify which parameters and return values share the same lifetime
	- Lifetime specifiers always start with `'`, like `'a, 'b, 'c`
- Static lifetimes
	- Static variable exists in a program from start to end
	- Static lifetime is a memory resources that will never be dropped
	- If static lifetime resources contain references, the must all be `'static`, since anything less than that wouldn't live long enough


## Text In Rust
- All literals are type `&'static str`
	- `&` means it's stored in a specific place in memory
	- `'static` means the string data will be available till the end of our program (never drops)
	- `str`: means that it points to a sequence of bytes that's always utf-8
- Strings would typically be placed in the data segment of your program memory
- Escape characters
	- See https://tourofrust.com/61_en.html
- Rust strings are multiline by default 
	- Use a `\` if we don't want a line break
- Raw strings can be created using `r#`
	- Lets us insert characters that might confuse a normal string as literals
- String literals can be taken from files using `include_str!()`
- Common methods in `&str`
	- `len`: gets the length of the string in bytes (not number of characters)
	- `starts_with`/`ends_with`: basic testing
	- `is_empty`: returns true if zero length
	- `find`: Returns an `Option<usize>` for the first position of some text
- Can convert utf-8 bytes to a vector of `chars` using `.collect`
	- A `char` in Rust is always 4 bytes long
- String struct in Rust
	- Stored on the heap, so it can be modified
	- `push_str` to add more utf-8 bytes
	- `replace` (self explanatory)
	- `to_lowercase`/`to_uppercase` (self explanatory)
	- `trim` for trimming space
	- When a string is dropped, its heap memory is also dropped
	- Text is passed to functions as a string slice to functions to avoid concerns surrounding ownership
- Other methods:
	- `concat` and `join`
- `format!` lets us format strings, similar to how you would in python with the f string
- Types can be converted to strings using `to_string`
- Certain values can also be parsed using `parse`
	- This returns a `Result` though since it could fail

## OOP in Rust
- No inheritance in Rust
- Methods are defined with an implementation block with keyword `impl`
```rust
impl MyStruct { 
    ...
    fn foo(&self) {
        ...
    }

	fn mutable_reference(&mut self) {
		...
	}
}
```
- `pub` exposes certain struct fields and methods
- Rust supports polymorphism with traits
```rust

trait NoiseMaker {
	fn make_noise(&self)
}

// Assume Sea Creature is defined 
impl NoiseMaker for SeaCreature {
	fn make_noise(&self) {
		println!("{}", &self.get_sound());
	}
}
```
- Traits can have certain implemented methods
- Traits can inherit from each other
- Dynamic vs. Static Dispatch
	- Static dispatch: When the instance type is known, we have direct knowledge of what function to call
	- Dynamic dispatch: When the instance type is not known, we must find out some way of calling the correct function
		- When using this, we preface the trait with `dyn` (like `&dyn MyTrait`)
		- This is slower because of the pointer chasing
- Box in Rust
	- Moves data from the stack to the heap
	- Holds a pointer to our data on the heap
	- Stores a reference in a struct that must know the size of its fields

## Smart Pointers
- Raw Pointers
	- Similar to a pointer in C, no restrictions on manipulation
	- `*const T`: constant pointer to data of type `T`
	- `*mut T`: mutable pointer 
	- Can access data with unsafe code
- Dereferencing
	- Used to access referred data during assignments of variables
	- Access to fields or methods of referred data
	- The `.` operator automatically dereferences a series of references
- References can be thought of as a higher-level type that gives access to another type
	- Smart pointers take this to another level by allowing the programmer to define how a particular struct can give access to another type
- Unsafe code primarily dereferences raw pointers. Smart pointers also typically dereference raw pointers extensively
- We can use `Box<dyn std::error::Error>` to define a return type that handles every possible error
	- `std::error::Error` is trait that all errors must implement

## Project Organization and Structure
- Every Rust program or library is a crate
- Every crate is made up of a hierarchy of modules
- Every crate has a root module
	- In programs, this is defined in `main.rs`
	- In libraries, this is defined in `lib.rs`
- A module can hold functions, traits, global variables, and other modules
- Creating modules (e.g, `foo`)
	- Either create a file called `foo.rs`
	- Or create a folder called `foo` and a `mod.rs` file within it
	- To establish a relationship between a submodule and its parent module, you must write `mod [sub-module];` in the parent module
- Make modules and functions accessible by declaring `pub`
- 