# Basic Calculator

## Problem

Evaluate a math expression given as a string: digits, `+`, `-`, and parentheses
at minimum (LeetCode has tiered versions: I adds parens, II adds `*`/`/`, III adds
both). The core technique is a stack-based expression parser: numbers and pending
operators/signs go on a stack, parentheses push/pop a "context."

## Why it's worth doing

Not an ownership problem like the linked-list stuff. This one's about string
parsing ergonomics: `chars().peekable()`, and parsing multi-digit numbers char by
char since there's no convenient slicing-while-you-scan. Good practice at the
part of Rust that has nothing to do with the borrow checker.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
