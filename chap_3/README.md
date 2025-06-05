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

<!--

## 3.3 Functions

## 3.4 Comments

## 3.5 Control Flow

-->