# Prefix Sum

## Prefix sum

```rust
fn build_prefix(arr: &[i32]) -> Vec<i32> {
    let mut prefix = vec![0; arr.len() + 1];

    for i in 0..arr.len() {
        prefix[i + 1] = prefix[i] + arr[i];
    }

    prefix
}

// sum of arr[left..=right]
fn range_sum(prefix: &[i32], left: usize, right: usize) -> i32 {
    prefix[right + 1] - prefix[left]
}
```

## Prefix sum + hashmap counting

```rust
use std::collections::HashMap;

// general shape: walk the array keeping a running sum, turn it into a
// "fingerprint" at each step, and ask a hashmap whether that fingerprint
// occurred before. A repeat means the subarray between the two points
// satisfies whatever property the fingerprint encodes.
//
// fingerprint swaps:
//   - sum - k   -> the subarray between the two points sums to exactly k
//   - sum % k   -> the subarray between the two points is divisible by k
//   - running sum with 0 mapped to -1 -> the subarray has equal 0s and 1s
//
// map value swaps:
//   - count      -> "how many subarrays end here with this property" (this fn)
//   - first index -> "how far back did this fingerprint last occur" (need length/distance)

// count subarrays summing to exactly k
fn subarray_sum_equals_k(arr: &[i32], k: i32) -> i32 {
    let mut seen: HashMap<i32, i32> = HashMap::new();
    seen.insert(0, 1); // empty prefix, so a subarray from index 0 can match

    let mut sum = 0;
    let mut count = 0;

    for &x in arr {
        sum += x;

        // fingerprint of the earlier prefix we need to have already seen;
        // swap for `sum % k` or a transformed running sum (0 -> -1 trick) for other variants
        let fingerprint = sum - k;

        // if this fingerprint occurred before, everything between here and there matches
        if let Some(&c) = seen.get(&fingerprint) {
            count += c;
        }

        *seen.entry(sum).or_insert(0) += 1;
    }

    count
}
```

## Problems

**Prefix sum**

- [Find Pivot Index](https://neetcode.io/problems/find-pivot-index/question?list=neetcode150) - Easy
- [Range Sum Query - Immutable](https://neetcode.io/problems/range-sum-query-immutable/question?list=neetcode150) - Easy
- [Count Vowel Strings in Ranges](https://neetcode.io/problems/count-vowel-strings-in-ranges/question?list=neetcode150) - Medium
- [Range Sum Query 2D - Immutable](https://neetcode.io/problems/range-sum-query-2d-immutable/question?list=neetcode150) - Medium
- [Product of Array Except Self](https://neetcode.io/problems/products-of-array-discluding-self/question?list=neetcode150) - Medium

**Prefix sum + hashmap counting**

- [Contiguous Array](https://leetcode.com/problems/contiguous-array/) - Medium
- [Subarray Sum Equals K](https://neetcode.io/problems/subarray-sum-equals-k/question?list=neetcode150) - Medium
- [Continuous Subarray Sum](https://neetcode.io/problems/continuous-subarray-sum/question?list=neetcode150) - Medium
