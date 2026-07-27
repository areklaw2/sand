# AVL Tree

Self-balancing BST: same operations as a plain BST, plus tracking height/balance
factor per node and rebalancing via rotations after insert/delete.

## Why worth building by hand

Same single-owner shape as `binary-search-tree`, but rotations are the
interesting part in Rust: to rotate you have to pull a subtree out of its
parent's `Option<Box<Node>>` (via `.take()`), rebuild the local structure, and
hand back a new owned subtree. Good concentrated exercise in "temporarily take
ownership away, then give something back", a pattern that shows up constantly
in Rust tree/list code once you notice it here.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
