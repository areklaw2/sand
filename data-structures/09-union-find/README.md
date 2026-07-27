# Union-Find (Disjoint Set)

`find(x)` / `union(x, y)` over a parent array, with path compression and
union by rank/size for near-O(1) amortized operations.

## Why worth building by hand

Purely array-based: two `Vec<usize>`s (parent, rank) and index arithmetic,
nothing else. One of the cleanest, most direct builds in this whole repo; good
one to do early for a confidence boost between the harder tree/allocator
exercises.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
