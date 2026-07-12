# Single-Threaded CPU

[LeetCode 1834](https://leetcode.com/problems/single-threaded-cpu/description/)

## Problem

Given tasks as `[enqueueTime, processingTime]` pairs, simulate a single-threaded
CPU: whenever it's idle and at least one task has arrived, it picks the
available task with the smallest processing time (ties broken by original
index). Return the order tasks are processed in.

## Approach shape

Sort tasks by enqueue time up front. Then it's a simulation loop: advance a
"current time" pointer, push every task that's arrived onto a min-heap keyed by
`(processing_time, original_index)`, pop the min each time the CPU goes idle. If
nothing's available yet, jump current time forward to the next task's enqueue
time.

## Why worth doing

Same heap-direction note as Design Twitter: `BinaryHeap` is a max-heap by
default, so pulling the *smallest* processing time out means ordering by
`Reverse` or negating. Otherwise this is a clean simulation problem with no
ownership fight. Ends up mostly testing whether the tie-breaking logic
(processing time, then index) is actually correct.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
