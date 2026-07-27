# Binary Heap

Array-based binary heap (min or max) built by hand, with sift-up on insert and
sift-down on extract-min/max, rather than reaching for `BinaryHeap`.

## Why worth building by hand

Mostly mechanical: array/index arithmetic (`parent = (i-1)/2`,
`children = 2i+1, 2i+2`), no ownership concerns at all. Useful mainly so the
std-library heaps used elsewhere in this repo (Design Twitter, Task Scheduler,
Single-Threaded CPU) stop being a black box.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
