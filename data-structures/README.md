# Data Structures

Hand-rolled implementations of the core data structures themselves, not the
patterns you reach for while solving a problem (those live in the `topics/`
write-ups), not a system built on top of one (that's `design-questions/`). This
is "build the thing `HashMap`/`Vec` already gives you, from scratch, to actually
understand what's inside it."

Each entry below is its own crate (`Cargo.toml`, `src/lib.rs`, `src/main.rs`,
`README.md`). `cd` into one and run `cargo test` or `cargo run`, or run
`cargo test -p <name>` from anywhere in the workspace.

## Roadmap

- [ ] `01-dynamic-array`: manual capacity growth, raw allocation in Rust
- [ ] `02-linked-list`: singly (`Box`, `Rc<RefCell<T>>`, arena) + doubly
      (`Rc<RefCell<T>>` + `Weak`, arena)
- [ ] `03-hash-map`: your own hashing + collision resolution (chaining or open
      addressing)
- [ ] `04-binary-search-tree`
- [ ] `05-avl-tree`: self-balancing, rotations
- [ ] `06-binary-heap`: array-based, manual sift-up/down (not `BinaryHeap`)
- [ ] `07-trie`
- [ ] `08-graph`: adjacency list and adjacency matrix representations
- [ ] `09-union-find`: disjoint set with path compression + union by rank
- [ ] `10-segment-tree`
- [ ] `11-b-tree`: multi-way search, split on insert, merge/borrow on delete
- [ ] `12-b-plus-tree`: `11-b-tree` plus linked leaves for range scans
