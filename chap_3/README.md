# 3. Common Programming Concepts

## 3.1 Variables and Mutability

By default, variables in Rust are immutable

### Constants

Similar to immutable variables, constants are not allowed to change. They have a few differences from variables:
- Constants are declared using the `const` keyword
- A constant's type must be annotated
- Constants can be declared in any scope, even globally
- Constants can only be set to the result of an expression (variables can be set to the result of something computed at runtime)
- Rust contention for constants is `UPPER_SNAKE_CASE`

### Shadowing

We can "shadow" a variable by reusing a variable name and repeating use of the `let` keyword.

This is allowed:

```rs
let x = 5;
let x = x + 1;
```

We can even do this:
```rs
let spaces = "   ";
let spaces = spaces.len();
```

## 3.2 Data Types

- The compiler can typically infer types by value or how it is used
- In cases where multiple types are possible, a type annotation is necessary (example: converting a string to a numeric type using `parse`)

### Scalar types

- A _scalar_ type represents a single value. Integers, floating-point numbers, booleans, and characters are scalar types.
- Rust's `char` type is its most primitive alphabetic type. `char` literals are specified with single quotes, in contrast to string literals which use double quotes.

### Compound types

- Compound types can group multiple values into one type. _Tuples_ and _arrays_ are Rust's two primitive compound types.
- A _tuple_ is a type for grouping a number of values of varied types into one compount type.
  - Tuples have a fixed length
  - Tuples are created via a comma-separated list of values inside a set of parentheses
  - example: `let tup: (i32, f64, u8) = (500, 6.4, 1);`
  - We can destructure from a tuple like `let (x, y, z) = tup;`
  - Tuple elements can also be accessed using `.` notation and the index of the value to access like `tup.0`
  - A tuple without any values is called a _unit_, written `()`. **Expressions implicitly return this value if they don't return any other.**
- An _array_ is a collection of multiple values of the same type.
  - Arrays in Rust have fixed lengths
  - Arrays allocate their data on the stack
  - A _vector_ is a similar collection but unlike the array can grow or shrink
  - If unsure whether to use an array or vector, its likely one should use a vector
  - Arrays are great when the number of elements won't change and can be known
  - Array syntax: `let a: [i32, 2] = [1, 2];`
  - Array elements can be accessed using `a[0]` syntax
  - Invalid array index access results in a panic at runtime

<!--

## 3.3 Functions

## 3.4 Comments

## 3.5 Control Flow

-->