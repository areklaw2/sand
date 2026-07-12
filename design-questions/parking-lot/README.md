# Parking Lot

## Problem

Classic OOD prompt: design a multi-level parking lot that supports different
vehicle sizes (motorcycle, car, bus) and spot sizes, assigns/frees spots, and
reports availability. There's no single "right" algorithm here. It's a class
design exercise.

## The Rust-specific decision this problem is really about

The textbook OOD answer reaches for inheritance without thinking about it: a
`Vehicle` base class, `Car`/`Motorcycle`/`Bus` subclasses overriding a
`spots_needed()` method, all stored in one list. Rust has no inheritance, so the
decision has to be made explicitly, between two options:

1. **`enum Vehicle { Car, Motorcycle, Bus }`**: closed set, exhaustive `match`
   everywhere, no dynamic dispatch. Good when the set of vehicle types is fixed
   and known at compile time (which, for an interview version of this problem,
   it always is).
2. **`trait Vehicle { fn spots_needed(&self) -> u32; }` + `Box<dyn Vehicle>`**:
   open to new vehicle types without touching existing code, costs a vtable
   indirection, closer in spirit to the inheritance version.

For this problem, (1) is almost always the better fit. The vehicle types are
fixed by the problem statement, not something a caller extends, and picking it
over (2) out of habit (because it's "the OOP way") is itself worth noticing.
Worth implementing both once to feel the difference before deciding.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Try the `enum` version first, then optionally add a `dyn Trait` version alongside
it to compare. Run `cargo test` or `cargo run` from inside this directory.
