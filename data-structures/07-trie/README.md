# Trie

Prefix tree supporting insert, search (exact match), and starts_with (prefix
match) over strings.

## Why worth building by hand

Single-owner tree again (each node owns its children), so it stays in safe,
straightforward Rust. The interesting decision is how children are stored: a
fixed-size array (`[Option<Box<Node>>; 26]` for lowercase-only) versus a
`HashMap<char, Box<Node>>` for arbitrary alphabets. Worth implementing one,
then considering when you'd reach for the other.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
