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

## 3.3 Functions

- `fn` keyword is used to declare functions
- Rust uses snake case as convention for function and variable names
- Rust doesn't care about the order that functions are defined, they just must be defined in a scope that can be seen by the caller
- Rust functions can have _parameters_. The concrete values callers provide for parameters are called _arguments_.
- The function's signature must declare the type of each parameter.
- Multiple function parameter declarations are separated by commas
- Function bodies are made up of statements and optionally end in an expression
  - **Statements** are instructions to perform an action, they do _not_ return a value
  - **Expressions** evaluate to a value

This is a _statement_:
```rs
let y = 6;
```

Statements don't return values, so this isn't valid:
```rs
let x = (let y = 6);
```

- In some languages like C or Ruby the assignment also _returns the value of the assignment_.

Consider this code:
```rs
{
    let x = 3;
    x + 1
}
```
The block ends in an expression that evaluates to `4`. We then could write code like this:
```rs
let y = {
    let x = 3;
    x + 1
};
```
As a result of this code the value `4` gets bound to `y`.

- **Expressions do not include an ending semicolon. A semicolon at the end of an expression turns it into a statement**
- Functions can return values. Return values aren't named, but we must declare a type for the return value using `-> TYPE` in the function's signature.
- In Rust, the return value of the function is the same as the value of the final expression in the function's body.
- We can return early using `return`
- Most functions return the last expression implicitly

## 3.4 Comments

- `//` are used for comments
- `//` can also be used at the end of lines containing code

## 3.5 Control Flow

### `if` Expressions

- Common `if SOME CONDITION {` syntax
- We can only use booleans in `if` expressions
- Rust also supports `else if` syntax
- Rust matches the first conditional and continues (e.g. `if`, `else if`, `else if` only the first matching conditional applies)

```rs
let number = 3;

if number < 5 {
    println!("condition was true");
} else {
    println!("condition was false");
}
```

#### `if` and `let`

`if` can be used in a `let` statement:
```rs
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

When used in such a context both blocks of code must result in the same type.

### Loops

- Rust includes three types of loops
  - `loop`
  - `while`
  - `for`

#### `loop`

- `loop` can be used to continually run code, until the program is stopped or `break` keyword is hit
- Rust also supports _loop labels_
- `continue` instructs Rust to skip the rest of the code in the current loop iteration and move on to the next iteration

```rs
fn main() {
    loop {
        println!("again!");
    }
}
```

The following construct can be used to return a value from a `loop` and capture it in a variable:

```rs
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

#### `while`

```rs
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

#### `for`

- Because of conciseness and safety `for` loops are the most commonly used looping construct in Rust

```rs
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

- `for` loops can also be used with a `Range`

```rs
fn main() {
    for number in (1..4) {
        println!("{number}!");
    }
}
```
