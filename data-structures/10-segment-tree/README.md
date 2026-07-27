# Segment Tree

Supports range queries (sum/min/max over a range) and point updates in
O(log n), typically built as a flat array where node `i`'s children are at
`2i+1` and `2i+2`.

## Why worth building by hand

Array/index-based like `union-find` and `binary-heap`. No ownership concerns.
Mainly useful as the "how do range queries actually work under the hood"
exercise, and a nice contrast with `08-trees`'s more general tree traversal
patterns.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
