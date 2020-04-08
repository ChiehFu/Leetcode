---
title: Smallest Number that is not a Sum of a Subset of List
tags: medium, Array
notebook: Leetcode
---

Given a sorted array (sorted in non-decreasing order) of positive numbers, find the smallest positive integer value that cannot be represented as sum of elements of any subset of given set.

Examples:
```c++
Input:  arr[] = {1, 3, 6, 10, 11, 15};
Output: 2

Input:  arr[] = {1, 1, 1, 1};
Output: 5

Input:  arr[] = {1, 1, 3, 4};
Output: 10

Input:  arr[] = {1, 2, 5, 10, 20, 40};
Output: 4

Input:  arr[] = {1, 2, 3, 4, 5, 6};
Output: 22
```
----------
Thoughts:
1. Scan through the array, and use `last` to represent the last number of the number `0 - last` that can be represented by the subarray `nums[0:i - 1]`.
2. For `nums[i]`, we can have two cases:
    1. If `nums[i]` is greater than `last` by `1`, which means `nums[i]` can continue the number `0 - last` and extend it to `0 - last + nums[i]`.
    2. Otherwise, if `nums[i]` is greater than `last` by more than `1`, there is a gap between `last` and `nums[i]`, which is `last + 1`, so `last + 1` will be the first number that can't be represented by the sum of the subarray of the input array.

```python
def findSmallest(nums):
    last = 0
    for num in nums:
        if num > last + 1:
            break
        else:
            last += num
    return last + 1
```
