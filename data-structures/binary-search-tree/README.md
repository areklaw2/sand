# Binary Search Tree

Standard unbalanced BST: insert, search, delete (including the two-children
case), in-order traversal.

## Why worth building by hand

Single-owner tree: each node is owned by exactly one parent, no
back-references needed, so `Option<Box<Node>>` maps onto it cleanly and this
is one of the more approachable builds in this folder. Good warm-up before
`avl-tree`, which needs the same shape plus rotations.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
