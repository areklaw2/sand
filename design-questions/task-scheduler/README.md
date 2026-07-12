# Task Scheduler

[LeetCode 621](https://leetcode.com/problems/task-scheduler/description/)

## Problem

Given a list of tasks (each a char/type) and a cooldown `n`, where the same task
type can't run again until `n` other units of time have passed (idle allowed),
find the minimum total time units to finish all tasks.

## Approach shape

Greedy: count frequency of each task type, repeatedly schedule the most frequent
remaining types first, leave idle slots where nothing is available. There's also
a closed-form version based on the max frequency and how many task types share
it, worth deriving once the heap-based greedy version works.

## Why worth doing

A max-heap-by-frequency drives the greedy choice, and here `BinaryHeap`'s
max-heap default is finally the direction you actually want, unlike the other
heap-based problems here. Good place to let the ordering pattern solidify rather
than re-derive it each time. No ownership issues.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
