# Linked List

Build the structure itself: a sequence of nodes where each node holds a value and
a link to the next one (and, for a doubly linked list, back to the previous one).
O(1) insert/remove given a node, O(n) index access, the inverse trade-off of a
dynamic array.

## What to implement

- **Singly linked list**: `push_front`, `pop_front`, `peek_front`, `len`,
  iteration, reverse.
- **Doubly linked list**: the above plus `push_back`/`pop_back` in O(1),
  `remove(node)` in O(1), and iteration in both directions.

| Struct                      | Storage                                          | Notes                                                                                                  |
| --------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `SinglyLinkedList<T>`       | `Option<Box<Node<T>>>`                           | plain owned, single-owner tree with one child                                                          |
| `SharedSinglyLinkedList<T>` | `Rc<RefCell<Node<T>>>`                           | the shape LeetCode-style problems hand you                                                             |
| `ArenaSinglyLinkedList<T>`  | `Vec<Node<T>>` + `Option<usize>` links           | index-based, free list for removed slots                                                               |
| `DoublyLinkedList<T>`       | `Rc<RefCell<Node<T>>>` + `Weak` back-pointers    | `Weak` on `prev` is what stops the cycle from leaking; runtime borrow panics instead of compile errors |
| `ArenaDoublyLinkedList<T>`  | `Vec<Node<T>>` + `Option<usize>` links both ways | what `topics/04-linked-lists` uses                                                                     |

## Traits design

One thin interface, implemented by all five, plus an extension trait for the
two that support O(1) back operations:

```rust
trait LinkedList<T> {
    fn push_front(&mut self, val: T);
    fn pop_front(&mut self) -> Option<T>;
    fn peek_front(&self) -> Option<&T>;
    fn len(&self) -> usize;
    fn is_empty(&self) -> bool { self.len() == 0 }
}

trait DoubleEndedLinkedList<T>: LinkedList<T> {
    fn push_back(&mut self, val: T);
    fn pop_back(&mut self) -> Option<T>;
    fn peek_back(&self) -> Option<&T>;
}
```

Run `cargo test` or `cargo run` from inside this directory.
