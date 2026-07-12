# Design Questions

Things like "Design Twitter," "Design a Parking Lot," or "LRU Cache" don't fit
under `topics/` as a single pattern. They're small systems/APIs that combine
several structures, where the interesting part is the interface design, not any
one data structure in isolation. That's a different skill from applying a single
pattern, so they get their own top-level category instead of living inside
`topics/`.

A few different flavors show up here, hard in Rust for different reasons:

- **Linked-structure caches** (LRU Cache, LFU Cache): built on top of the
  arena/doubly-linked-list pattern written up in `topics/04-linked-lists/README.md`
  (the same pattern the `linked-list` crate under `data-structures/` will
  eventually implement), plus extra bookkeeping (recency order, frequency
  buckets) on top.
- **Multi-structure API design** (Design Twitter, Browser History, a rate
  limiter): the challenge is combining a heap/map/set/stack cleanly behind a
  small API, not any ownership fight in particular.
- **String/expression parsing** (Basic Calculator): stack-based parsing, mostly
  about Rust's char-handling ergonomics.
- **Object-oriented design** (Parking Lot, Vending Machine, Elevator System):
  the challenge is that Rust has no class inheritance. "A `Car` and
  `Motorcycle` are both `Vehicle`s" has to become either a `trait` +
  `dyn Trait`/generics, or an `enum` with variants. Picking between those two
  is most of the design work. Closer to the trait/aggregate-boundary thinking
  from [[volt]] than to algorithm templates.
- **Scheduling/simulation** (Single-Threaded CPU, Task Scheduler): greedy +
  heap problems, no ownership fight, just the same `BinaryHeap`-is-a-max-heap
  ordering trick that shows up in Design Twitter too.

## Contents

Each of these is its own crate (`Cargo.toml`, `src/lib.rs`, `src/main.rs`,
`README.md`). All scaffolded, no solutions, these are yours to build:

- `lru-cache/`
- `lfu-cache/`
- `design-twitter/`
- `browser-history/`
- `basic-calculator/`
- `parking-lot/`
- `single-threaded-cpu/`
- `task-scheduler/`

## Roadmap (not yet scaffolded)

- [ ] Vending Machine
- [ ] Elevator System
- [ ] Tic-Tac-Toe / generic board game
- [ ] In-memory File System
- [ ] Rate Limiter (ties into [[volt]]'s API layer if you want a real use for it)
