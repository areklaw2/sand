# Linked Lists

## Subtopics

- [x] Fast and Slow Pointer
- [x] Doubly Linked List
- [x] LRU Cache
- [x] LFU Cache
- [x] HashMap/HashSet-backed structures (see LRU/LFU, that's the point of both)

## Why this topic is the whole point of the repo

Every other topic is mostly mechanical once you know the pattern. Linked lists
are where that breaks down. In a garbage-collected language, nodes just hold
direct references to their neighbors and the runtime cleans up whatever nothing
points to anymore. Rust's borrow checker won't let two `Node` structs hold live mutable
references to each other. You can't express "this node owns the next node, which
also needs to point back at this node."

The fix used throughout is the **arena / index pattern**: instead of `Node` structs
holding `Box<Node>` or `&Node` pointers to each other, they live in a flat
`Vec<Node>` and refer to each other by `usize` index. No lifetimes to fight, no
`Rc<RefCell<T>>` runtime borrow checks, just a vector and integers. This is also
closer to what you'd actually reach for in production Rust (see `slotmap` /
`generational-arena` for a hardened version of the same idea).

## Where the code lives

Nothing in `topics/` compiles. The snippets below are reference text. Read them,
then write the real thing where it can be tested:

- **`data-structures/linked-list/`**: the structure for its own sake. Full API,
  removal, free-list reuse, and all three answers to the doubly-linked problem
  (arena, `Rc<RefCell<T>>` + `Weak`, raw pointers).
- **`design-questions/lru-cache/`** and **`lfu-cache/`**: the doubly-linked list
  put to work, with move-to-front and eviction on top.

Both are crates. `cargo test` from inside either one.

## Snippets

### Singly linked list

Ownership only ever flows one direction: head owns the next node, which owns the
next, so no back-references are needed and `Option<Box<Node>>` covers it.

```rust
pub struct Node<T> {
    pub value: T,
    pub next: Option<Box<Node<T>>>,
}

pub struct LinkedList<T> {
    head: Option<Box<Node<T>>>,
}

impl<T> LinkedList<T> {
    pub fn new() -> Self {
        LinkedList { head: None }
    }

    pub fn push_front(&mut self, value: T) {
        let new_node = Box::new(Node {
            value,
            next: self.head.take(),
        });
        self.head = Some(new_node);
    }

    pub fn pop_front(&mut self) -> Option<T> {
        self.head.take().map(|node| {
            self.head = node.next;
            node.value
        })
    }

    pub fn to_vec(&self) -> Vec<&T> {
        let mut out = Vec::new();
        let mut cur = &self.head;
        while let Some(node) = cur {
            out.push(&node.value);
            cur = &node.next;
        }
        out
    }
}
```

The catch this snippet hides: the derived `Drop` is recursive, so dropping a long
list can blow the stack. Writing an iterative `Drop` is part of what
`data-structures/linked-list/` asks for.

### Doubly linked list (arena)

The direct version is impossible: `prev` and `next` would each need a live mutable
reference back to a shared neighbor. Nodes live in a `Vec` instead, linked by index.

```rust
pub struct Node<T> {
    pub value: T,
    pub prev: Option<usize>,
    pub next: Option<usize>,
}

pub struct DoublyLinkedList<T> {
    nodes: Vec<Node<T>>,
    head: Option<usize>,
    tail: Option<usize>,
}

impl<T> DoublyLinkedList<T> {
    pub fn new() -> Self {
        DoublyLinkedList {
            nodes: Vec::new(),
            head: None,
            tail: None,
        }
    }

    /// Returns the index of the newly inserted node.
    pub fn push_front(&mut self, value: T) -> usize {
        let idx = self.nodes.len();
        self.nodes.push(Node {
            value,
            prev: None,
            next: self.head,
        });
        if let Some(h) = self.head {
            self.nodes[h].prev = Some(idx);
        }
        self.head = Some(idx);
        if self.tail.is_none() {
            self.tail = Some(idx);
        }
        idx
    }

    pub fn value(&self, idx: usize) -> &T {
        &self.nodes[idx].value
    }
}
```

`push_front` only, enough to show the arena shape. `remove(idx)` and a free list
so removed slots get reused instead of the `Vec` growing forever are exactly what
the `linked-list` crate is for.

### Fast/slow pointer (Floyd's)

Generalized over any `next` function. Translates cleanly because it operates on
plain values and indices, never on borrowed node references.

```rust
pub fn has_cycle<T, F>(start: T, next: F) -> bool
where
    T: PartialEq + Copy,
    F: Fn(T) -> T,
{
    let mut slow = start;
    let mut fast = start;
    loop {
        slow = next(slow);
        fast = next(next(fast));
        if slow == fast {
            return true;
        }
        // Assumes a cycle exists, or that the caller adds a termination condition.
    }
}
```

## Problems

One markdown file per problem in `problems/`: description, link, and solution.
