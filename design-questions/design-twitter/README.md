# Design Twitter

## Problem

Implement a simplified Twitter with:
- `post_tweet(user_id, tweet_id)`
- `get_news_feed(user_id)`: the 10 most recent tweet ids from the user and everyone
  they follow, most recent first
- `follow(follower_id, followee_id)`
- `unfollow(follower_id, followee_id)`

## What's actually interesting about this one

Unlike the linked-list problems, there's no ownership fight here. The underlying
data is just plain values in `Vec`s/`Map`s/`Set`s, nothing self-referential. The
interesting part is API and heap ergonomics: `BinaryHeap` is a max-heap, so
merging the k most recent tweets means ordering by `Reverse` or negating.

## Status

Not started. This is a crate:

```
src/lib.rs    # the implementation
src/main.rs   # scratch entrypoint, `cargo run` from this directory
```

Run `cargo test` or `cargo run` from inside this directory.
