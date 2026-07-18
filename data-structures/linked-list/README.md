# Linked List

Build the structure itself: a sequence of nodes where each node holds a value and
a link to the next one (and, for a doubly linked list, back to the previous one).
O(1) insert/remove given a node, O(n) index access, the inverse trade-off of a
dynamic array.

## What to implement

- **Singly linked list**: `push_front`, `push_back`, `pop_front`, `insert_after`,
  `remove_after`, `len`, iteration, reverse.
- **Doubly linked list**: the above plus `push_back`/`pop_back` in O(1),
  `remove(node)` in O(1), and iteration in both directions.

## The Rust part

Splits across the two tiers from `../README.md`:

- **Singly linked** is a single-owner tree with one child: `Option<Box<Node>>`,
  no back-references, so it stays simple. The interesting bits are
  `Option::take()` for unlinking and why a recursive `Drop` can blow the stack on
  a long list (write an iterative `Drop`).
- **Doubly linked** is the structure the borrow checker exists to reject: two
  nodes each holding a live mutable reference to the other. Three ways out, in
  the order this repo prefers them:
  1. **Arena / index-based**: nodes in a `Vec<Node>`, `Option<usize>` links, a
     free list for removed slots. What `topics/04-linked-lists` uses.
  2. **`Rc<RefCell<T>>` + `Weak` back-pointers**: the closest thing to a direct
     pointer design; `Weak` on `prev` is what stops the cycle from leaking.
     Runtime borrow panics instead of compile errors.
  3. **Raw pointers + `unsafe`**: what `std::collections::LinkedList` actually
     does. Worth reading its source after writing your own.

Doing all three of these on the same structure is the single best exercise in the
repo for the ownership problem the root README is about.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
