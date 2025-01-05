## Structs in C
- User-defined, structured group of variables
- Purpose of struct definitions are so that the compiler knows the size and layout of an instance of the struct
- Fields are accessed using the `.` operator, though when dealing with pointers to structs, we can dereference and access fields with `->`
- Fields are ordered according to the declaration order, even if another order would be more compact

## Typedef in C
- Allows us to create aliases to types
- Example: `type unsigned int uint;`
- Can use it with structs in the following way:
```C
struct point_st {
  int x;
  int y;
};
typedef struct point_st Point;
Point pt1;

// Or 

typedef struct {
	int x;
	int y;
} Point2;
Point2 pt2;
```

## Aligned Data
- Primitive data type requires `K` bytes
- Address must be a multiple of `K`
- Required on some machines; advised on x86-64

## Motivation for aligning data
- Memory accessed by aligned chunks of bytes
	- Important for caching and paging, virtual memory
	- Inefficient to load or store value that spans quad word boundaries

![[Pasted image 20241025150745.png]]



[[Lecture 13 - Executables and Arrays]]
[[Lecture 1 - Introduction, Binary]]