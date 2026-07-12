# Dynamic Array

Build what `Vec` already gives you: contiguous storage that grows as
needed (typically doubling capacity when full), with O(1) amortized push and
O(1) index access.

## Why this is the hard one

Every other structure in this folder has a reasonably clean safe-Rust version.
This one doesn't. A real dynamic array needs manually managed, uninitialized
memory that you grow and reallocate yourself, which safe Rust doesn't expose.
That means `std::alloc::{alloc, dealloc, realloc}`, raw pointers, and `unsafe`
blocks for reads/writes into that memory. It's the one structure here with no way
to dodge the low-level details. Worth doing after the others, since it's a
genuinely different (and more involved) exercise.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
