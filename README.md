# Sand

**S**tructures, **A**lgorithms, a**N**d **D**esign.

## Structure

Three top-level categories:

- `topics/`: one algorithmic pattern per folder. Documentation only, no code.
- `data-structures/`: the core structures built by hand (your own hash map, heap,
  trie), not tied to any specific problem. See `data-structures/README.md`.
- `design-questions/`: things like Design Twitter or a Parking Lot. Small systems
  combining several structures behind an API, not a single pattern. See
  `design-questions/README.md`.

Each topic under `topics/` is intended to look like this.

```
topics/NN-topic-name/
  README.md              # the pattern, with Rust snippets inline
  problems/
    problem-name.md      # description + link + solution
```

Each crate under `data-structures/` and `design-questions/`:

```
data-structures/hash-map/     # and each of the other 17 crates
  Cargo.toml
  src/lib.rs
  src/main.rs
  README.md
```

## Working in the repo

`data-structures/` and `design-questions/` are a Cargo workspace, one crate each,
18 in total. `topics/` is documentation and contains no code.

```bash
cargo build --workspace          # everything
cargo test -p hash-map           # one crate, from anywhere

cd data-structures/hash-map
cargo test                       # scopes to this crate
cargo run                        # src/main.rs, a scratch pad for poking at it
```
