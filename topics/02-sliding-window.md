# Sliding Window

## Fixed-size window

```rust
fn fixed_window(arr: &[i32], k: usize) -> i32 {
    let mut window_sum = 0;
    let mut best = i32::MIN;

    for i in 0..arr.len() {
        window_sum += arr[i];

        if i >= k - 1 {
            // window is exactly k wide, arr[i - k + 1..=i]
            best = best.max(window_sum);
            window_sum -= arr[i - (k - 1)];
        }
    }

    best
}
```

## Dynamic window

```rust
fn dynamic_window(arr: &[i32]) -> i32 {
    let mut left = 0;
    let mut state = 0;
    let mut best = 0;

    for right in 0..arr.len() {
        // grow: fold arr[right] into state
        state += arr[right];

        while /* window at [left, right] is invalid? */ false {
            // shrink: peel arr[left] out of state
            state -= arr[left];
            left += 1;
        }

        best = best.max(right - left + 1);
    }

    best as i32
}
```

## Dynamic window with flips

```rust
fn dynamic_window_with_flips(arr: &[i32], max_flips: i32) -> i32 {
    let mut left = 0;
    let mut flips = 0;
    let mut best = 0;

    for right in 0..arr.len() {
        // entering the window cost a flip? (e.g. arr[right] is the "wrong" value)
        if /* arr[right] needs a flip? */ false {
            flips += 1;
        }

        while flips > max_flips {
            // shrinking past a flipped element refunds it
            if /* arr[left] was a flip? */ false {
                flips -= 1;
            }
            left += 1;
        }

        best = best.max(right - left + 1);
    }

    best as i32
}
```

## Counting windows with exactly K distinct (at-most-K trick)

```rust
use std::collections::HashMap;

// exact(k) = at_most(k) - at_most(k - 1)
// counting windows with EXACTLY k of something is hard directly, but
// "at most k" is a normal dynamic window, and the difference of two
// at-most windows is exactly the count you want.
fn exact_k(arr: &[i32], k: i32) -> i32 {
    at_most_k(arr, k) - at_most_k(arr, k - 1)
}

fn at_most_k(arr: &[i32], k: i32) -> i32 {
    if k < 0 {
        return 0;
    }

    let mut count: HashMap<i32, i32> = HashMap::new();
    let mut left = 0;
    let mut windows = 0;

    for right in 0..arr.len() {
        *count.entry(arr[right]).or_insert(0) += 1;

        while count.len() as i32 > k {
            // shrink until at most k distinct values remain
            let d = arr[left];
            *count.get_mut(&d).unwrap() -= 1;
            if count[&d] == 0 {
                count.remove(&d);
            }
            left += 1;
        }

        // every window ending at `right` and starting in [left, right] qualifies
        windows += (right - left + 1) as i32;
    }

    windows
}
```

## Problems

**Fixed-size window**

- [Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/) - Easy
- [Sliding Window Maximum](https://neetcode.io/problems/sliding-window-maximum/question?list=neetcode150) - Hard (needs monotonic deque)

**Dynamic window**

- [Best Time to Buy and Sell Stock](https://neetcode.io/problems/buy-and-sell-crypto/question?list=neetcode150) - Easy
- [Longest Substring Without Repeating Characters](https://neetcode.io/problems/longest-substring-without-duplicates/question?list=neetcode150) - Medium
- [Minimum Size Subarray Sum](https://neetcode.io/problems/minimum-size-subarray-sum/question?list=allNC) - Medium

**Dynamic window with flips**

- [Longest Repeating Character Replacement](https://neetcode.io/problems/longest-repeating-substring-with-replacement/question?list=neetcode150) - Medium
- [Max Consecutive Ones III](https://neetcode.io/problems/max-consecutive-ones-iii/question?list=allNC) - Medium

**Counting windows with exactly K distinct (at-most-K trick)**

- [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/) - Medium
- [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/) - Hard

**Miscellaneous**

- [Permutation in String](https://neetcode.io/problems/permutation-string/question?list=neetcode150) - Medium
- [Minimum Window Substring](https://neetcode.io/problems/minimum-window-with-characters/question?list=neetcode150) - Hard
