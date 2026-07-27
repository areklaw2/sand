# B+ Tree

Same shape as `11-b-tree` for the internal nodes — multi-way search, split on
insert, borrow/merge on delete — but keys only route at internal nodes; every
value lives in a leaf, and leaves are threaded together left-to-right for
O(k) range scans. What most real database indexes (PostgreSQL, InnoDB)
actually use, not the plain B-Tree.

## Why worth building by hand

The leaf-linking is the reason this gets its own crate instead of a flag on
`11-b-tree`: internal nodes stay `Vec<Box<Node<T>>>`, single-owner, but each
leaf needs a `next` pointer to a sibling leaf that's owned by the tree's leaf
chain, not by the leaf's parent — the same ownership problem `02-linked-list`
solves with `Rc<RefCell<T>>`/arena, this time showing up inside a tree
instead of standing on its own.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
