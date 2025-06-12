# 4. Understanding Ownership

Ownership is Rust’s most unique feature, it enables Rust to make memory safety guarantees without needing a garbage collector.

- _Ownership_ is a set of rules that govern how a Rust program manages memory.
  - If the rules are violated, the program won't compile
- Ownership can be thought of as an alternative approaches like garbage collection or manually allocated memory

## Stack and Heap

- Many languages don't require the programmer to think about the stack and heap
- For systems languages like Rust, whether a value is on the stack or heap can affect how the language behaves (and _should_ impact how the developer writes code!)
- Stack and heap are parts of memory
  - The stack stores values in order and is operated on with pushes and pops
  - The heap, in contrast, is less organized. Space is _allocated_, and a _pointer_ is returned which points at the location of the memory.
  - Pushing to the stack is faster than allocating on the heap (because the allocator doesn't need to search for a space, it always stores at the top of the stack)
  - Accessing data in the heap is slower than accessing data on the stack (because you have to follow a pointer to get there)
  - When a function is called, the values passed to the function (even pointers to data on the heap) and the function's local variables get pushed onto the stack
    - When the function exits, the values get popped off the stack

## Ownership Rules

- Each value in Rust has an owner
- There can only be one owner at a time
- When the owner goes out of scope, the value will be dropped

## Variable Scope

- Variable _scope_ is the range within a program for which an item is valid