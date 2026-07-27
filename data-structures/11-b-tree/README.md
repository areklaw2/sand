# B-Tree

Self-balancing multi-way search tree: each node holds up to `m - 1` keys and
up to `m` children (order `m`), staying shallow by fanning out instead of
going deeper. Search, insert (split a full node, push the median key up to
the parent), delete (merge with or borrow from a sibling to keep every node
at least half full).

## Why worth building by hand

Still a single-owner tree (`Vec<Box<Node<T>>>` children, no back-references),
but multi-way instead of binary: insert has to report "I split, here's the
new sibling and the key that moved up" back to the caller, which recurses one
level higher and might split _that_ node too, all the way to a new root.
Different exercise from `04-binary-search-tree`/`05-avl-tree`'s single-child
rotations — this is propagating a structural change upward through owned
parents, not rotating a fixed shape.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
