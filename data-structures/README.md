# Data Structures

Hand-rolled implementations of the core data structures themselves, not the
patterns you reach for while solving a problem (those live in the `topics/`
write-ups), not a system built on top of one (that's `design-questions/`). This
is "build the thing `HashMap`/`Vec` already gives you, from scratch, to actually
understand what's inside it."

Each entry below is its own crate (`Cargo.toml`, `src/lib.rs`, `src/main.rs`,
`README.md`). `cd` into one and run `cargo test` or `cargo run`, or run
`cargo test -p <name>` from anywhere in the workspace.

No equivalent section for algorithms: an algorithm's hand-written
implementation *is* its template, so there's nothing extra to build; this
category only makes sense for structures.

## Why these split into four very different difficulty tiers in Rust

- **Already index/array-based when you build it properly**: Hash Map,
  Union-Find, Segment Tree, Binary Heap. The "correct" implementation was never
  going to use object references between elements anyway, so the borrow checker
  never enters into it. Union-Find especially: it's just two arrays.
- **Single-owner trees**: Binary Search Tree, AVL Tree, Trie. Each node is
  owned by exactly one parent (`Option<Box<Node>>`), no back-references needed,
  so these stay in safe, straightforward Rust too, though AVL's rotations are a
  good `Option::take()` exercise, since you have to pull a node out of its parent's
  ownership, rebuild the subtree, and put something back.
- **The mutually-referencing one**: Linked List. A singly linked list is
  single-owner and stays simple; a doubly linked list is the exact thing the
  borrow checker refuses (two nodes each pointing at the other), so it needs an
  arena, `Rc<RefCell<T>>` + `Weak`, or `unsafe`. See `linked-list/README.md`.
- **The one that actually needs `unsafe`**: Dynamic Array. Implementing your
  own `Vec` properly (manual capacity growth, raw memory allocation) is the one
  case here with no safe and obvious version. You end up reaching for
  `std::alloc` and raw pointers just to get the same behavior `Vec` gives you for
  free. Worth doing last, once the others feel comfortable.

Linked List also appears in `topics/04-linked-lists/README.md`, but as
scaffolding for that topic's patterns (minimal API, `push_front` only in the
inline snippet). Here it's the structure itself: full API, removal, free-list
reuse. Same split as `dynamic-array` vs. reaching for `Vec` in every other topic.

## Roadmap

- [ ] `dynamic-array`: manual capacity growth, raw allocation in Rust
- [ ] `linked-list`: singly + doubly; arena, `Rc<RefCell<T>>`, and `unsafe`
      versions of the doubly linked one
- [ ] `hash-map`: your own hashing + collision resolution (chaining or open
      addressing)
- [ ] `binary-search-tree`
- [ ] `avl-tree`: self-balancing, rotations
- [ ] `binary-heap`: array-based, manual sift-up/down (not `BinaryHeap`)
- [ ] `trie`
- [ ] `graph`: adjacency list and adjacency matrix representations
- [ ] `union-find`: disjoint set with path compression + union by rank
- [ ] `segment-tree`
