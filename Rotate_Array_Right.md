# Rotate Array - Leetcode 189

## Problem Statement

Given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

Follow up:
Try to come up with as many solutions as you can. There are at least three different ways to solve this problem.
Could you do it in-place with O(1) extra space?

### Example

```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]  
```

Constraints:
1 <= nums.length <= 10^5
-2^31 <= nums[i] <= 2^31 - 1
0 <= k <= 10^5

---

## Problem Understanding (in words)

Given an integer array `nums` and non-negative integer `k`, the task is to rotate the array to the right by `k` positions.

Rotating by 1 position means:
* last element moves to the front
* all other elements shift one position to the right

To rotate the array by `k` positions means repeating this process k times.

The relative order of elements should be preserved while rotating the array.

Also, check whether this can be done in-place, that is without using extra space by just modifying original array. 

Now, according to the constraints: 
* The array can be large, so solutions that repeatedly shift elements one by one may become inefficient. 
* Values can be large, but here size of elements doe snot affect the rotation logic so that is fine. 
* `k` can be greater than the array length, so hnadling large k values must be done.

---
