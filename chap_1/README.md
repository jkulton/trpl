# 1. Getting started

## 1.2 Hello world

```rs
fn main() {
    println!("Hello, world!");
}
```

- The `main` function is special: it is always the first code that runs in every executable Rust program.
- `println!()` calls a _macro_, not a normal function. The `!` indicates the call to a macro.

(From same directory)
```
$ rustc main.rs
$ ./main
Hello, world!
```

## 1.3 Hello, Cargo!

- Cargo (`cargo`) is Rust's build system and package manager
- Create a new project: `cargo new hello_cargo`
  - Skip vcs with `--vcs none`
- Cargo expects source files to live inside a `src` directory
- (from within `/hello_cargo`)
  - Build: `cargo build`
  - Run: `cargo run`
  - Compile without producing executable: `cargo check`

---

## Unsorted notes

- Ruby-like things:
  - Implicitly returns the last expression of a function's body
  - `(1..4)` syntax for ranges
  - Naked conditions `if number > 0` ...

- C-like language things:
  - Lots of `{}`

- Go-like in these ways:
  - `main.go` vs `main.rs`
    - `main` function always runs first
  - `cargo build && cargo run`
  