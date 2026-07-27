# Hash Map

Build what `HashMap` already gives you: a hash function, buckets, and a
collision resolution strategy (separate chaining is the simpler starting
point; open addressing with probing is the harder follow-up), plus resizing
once the load factor gets too high.

## Why worth building by hand

Your own map has to declare `K: Hash + Eq` (or implement its own hash function)
as a trait bound up front, which forces the hashing and equality contract into
the type signature instead of leaving it implicit. Good exercise in generic trait
bounds beyond DSA specifically.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
