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

### More on scope, via complex data with `String`
- Complex types are stored on the heap rather than the stack. In contrast to a string literal, `String` is a complex data type.

### Memory and Allocation

- A string literal, since its contents are known at compile time, is hardcoded directly into the program's executable
- With the `String` type we instead allocate some memory on the heap to hold the contents
- Importantly, we need to do two things:
  - Request memory from the allocator at runtime
  - Return memory to the allocator when we're done
- The first step is handled via `String::from`
- In languages with a garbage collector (GC), the GC tracks and cleans up memory that is unused, and we need not think about it. In most languages without a GC, its on the programmer to identify when memory is no longer used and explicitly free the memory
- In Rust, the memory is automatically returned once the variable that owns the memory goes out of scope
  - This happens via Rust calling a special function, `drop`, automatically

### Variables and Data Interacting with Move

Contrast these two examples:

```rs
let x = 5;
let y = x;
```

In this example `x` and `y` are separate variables both equal to `5`.

vs

```rs
let s1 = String::from("hello");
let s2 = s1;
```

This example includes something called a _move_, where `s2` now points at the value originally pointed at by `s1`, and `s1` is now invalidated.

**Rust will never automatically create "deep" copies of data.**

### Scope and Assignment

- When we assign a new value to an existing variable Rust will call `drop` and free the original value's memory immediately

### Variables and Data Interacting with Clone

- In order to deeply copy heap data we can use the `clone` method

### Stack-Only Data: Copy

```rs
  let x = 5;
  let y = x;

  println!("x = {x}, y = {y}");
```

Note that `x` is not _moved_ to `y`, because this is stack-based data it can be copied more efficiently

- Rust has a annotation called the `Copy` trait which can be placed on types that are stored on the stack. It s type implements `Copy` variables that use it do not _move_, but are trivially copied
- In contrast, Rust will not let a type be annotated with `Copy` if the type or any of its parts implement the `Drop` trait

Some types that implement `Copy`:
- Integer types
- Boolean type
- Floating-point types
- Character type
- Tuples

### Ownership and Functions

- Passing a value to a function works similarly to assigning values to variables
- Passing a variable to a function will either move or copy, just like assignment

## References and Borrowing

Using the `&` notation (_referencing_) we can pass a reference to a function:

```rs
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{s1}' is {len}.");
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

- The opposite of referencing is _dereferencing_, accomplished with `*`, the dereference operator.
- When we create a reference, it _refers_ to the value but does not own it.
- The action of creating a reference is called _borrowing_
- References are immutable by default
- A mutable reference can be created with `& mut VARIABLE`, similarly a function's signature must use `&mut SOME_TYPE` notation
  - Only one borrowed mutable of a value can exist at once
  - Similarly a value cannot be borrowed as both mutable and immutable at the same time

### Dangling References

- A _dangling pointer_ is a pointer that references a location whose memory has been freed
- Rust's compiler prevents dangling pointers

### Rules of References

- At a given time we may have one mutable reference or any number of immutable references to a value
- References must always be valid