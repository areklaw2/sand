# Browser History

## Problem

Design a browser history with `visit(url)`, `back(steps)`, and `forward(steps)`.
Visiting a new page clears all forward history from the current point, the way a
real browser does.

## Approach shape

Two stacks (back-stack, forward-stack) or a single array with a current-position
pointer, clearing everything past that pointer on `visit`. Either way it's simpler
than it sounds. No self-referential node structures involved, so it's a decent
"design an API cleanly" exercise rather than an ownership-fight one.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
