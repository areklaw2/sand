# LRU Cache

## Problem

Design a fixed-capacity cache supporting `get(key)` and `put(key, value)`, both in
O(1), that evicts the **least recently used** entry when it's full. Both `get` and
`put` count as "using" a key and should refresh its position.

## Why it's harder in Rust

The usual approach needs a hash map (key -> node) plus a doubly linked list
ordering nodes from most- to least-recently-used. The map gives O(1) lookup, the
list gives O(1) reordering. The naive version of that (nodes holding
`prev`/`next` references straight to each other) is exactly the shape Rust's
borrow checker rejects: two nodes can't each hold a live mutable reference to a
neighbor that also references them back.

The general fix worth knowing about going in: an arena/index-based structure
(nodes in a `Vec`, linked by `usize` index instead of pointer) sidesteps the
problem entirely. See the doubly-linked-list snippet in
`topics/04-linked-lists/README.md` for that pattern in isolation before applying
it here.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Write the obvious version first, the way it'd naturally come together, then
work through the ownership issue above to get it past the borrow checker. Run
`cargo test` or `cargo run` from inside this directory.
