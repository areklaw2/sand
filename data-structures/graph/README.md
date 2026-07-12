# Graph

Both common representations: adjacency list and adjacency matrix, plus basic
traversal (BFS/DFS) over each to confirm they behave the same.

## Why worth building by hand

Unlike linked lists, graphs are usually represented by vertex *indices* even
in the "obvious" version (`Vec<Vec<usize>>` for adjacency list) rather than
objects holding direct references to each other, so the natural representation
already sidesteps the ownership problem entirely. Good contrast to point out
after the linked-list topic: the ownership fight isn't inherent to "things that
reference each other," it's
specific to *object-graph-shaped* references. Index-based structures were
fine all along.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
