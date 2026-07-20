# Two Pointers

## Two Pointers: left/right (classic)

```rust
fn two_pointer(arr: &[i32]) -> i32 {
    let mut left = 0;
    let mut right = arr.len().saturating_sub(1);
    let mut ans = 0;

    while left < right {
        // inspect/update state using arr[left] and arr[right]
        if /* shrink from the left? */ true {
            left += 1;
        } else {
            right -= 1;
        }
    }

    ans
}
```

## Two Pointers: slow/fast

```rust
fn two_pointer_slow_fast(arr: &mut [i32]) -> i32 {
    let mut slow = 0;

    for fast in 0..arr.len() {
        // slow marks the write position; fast scans ahead looking for a keeper
        if /* arr[fast] should be kept? */ true {
            arr[slow] = arr[fast];
            slow += 1;
        }
    }

    slow as i32
}
```

## Two Pointers: two arrays

```rust
fn two_pointer_two_arrays(arr1: &[i32], arr2: &[i32]) -> i32 {
    let mut i = 0;
    let mut j = 0;
    let mut ans = 0;

    while i < arr1.len() && j < arr2.len() {
        // compare/combine arr1[i] and arr2[j], then advance whichever pointer lost out
        if /* arr1[i] takes priority? */ true {
            i += 1;
        } else {
            j += 1;
        }
    }

    while i < arr1.len() {
        // handle whatever's left in arr1
        i += 1;
    }
    while j < arr2.len() {
        // handle whatever's left in arr2
        j += 1;
    }

    ans
}
```

## Problems

**Left/right (classic)**

- [Valid Palindrome](https://neetcode.io/problems/is-palindrome/question?list=neetcode150) - Easy
- [3Sum](https://neetcode.io/problems/three-integer-sum/question?list=neetcode150) - Medium
- [Container With Most Water](https://neetcode.io/problems/max-water-container/question?list=neetcode150) - Medium
- [Trapping Rain Water](https://neetcode.io/problems/trapping-rain-water/question) - Hard

**Slow/fast**

- [Remove Duplicates From Sorted Array](https://neetcode.io/problems/remove-duplicates-from-sorted-array/question?list=allNC) - Easy

**Two arrays**

- [Merge Sorted Array](https://neetcode.io/problems/merge-sorted-array/question?list=allNC) - Easy
