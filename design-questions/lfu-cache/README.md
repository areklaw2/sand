# LFU Cache

## Problem

Like LRU, but eviction is based on **least frequently used**, with least-recently-used
as the tiebreaker among entries sharing the minimum frequency. `get`/`put` both count
as a "use" and bump the frequency count.

## Why it's harder than LRU in Rust

LRU only needs one ordered structure (the doubly linked list). LFU needs an ordered
structure *per frequency bucket* (for the recency tiebreak), plus a running
`min_freq` and a key -> frequency lookup, all kept in sync on every access. Getting
each frequency bucket down to true O(1) insert/remove/evict means combining the
arena/index pattern from the LRU cache with a second layer of indexing by
frequency. Worth attempting the straightforward (if not fully O(1)) version first.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
