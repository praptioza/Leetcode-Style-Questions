# Two Sum — LeetCode #1

## Problem Statement

Given an array of integers `nums` and an integer `target`, **return the indices of the two numbers** such that they add up to `target`.
You may assume that *each input has exactly one solution*, and *you may not use the same element twice*.
Return the answer in any order. ([LeetCode][1])

### Example

```
Input: nums = [2,7,11,15], target = 9  
Output: [0,1]  
Explanation: nums[0] + nums[1] == 9  
```

---

## Problem Understanding (in words)

You are given a list of integers and a target number.
You must find **two distinct elements** in the list whose values sum to exactly the target.
You should return their *indices* (not the values).
There’s always exactly one correct pair. ([LeetCode][1])

---

## High-Level Approaches Considered

**1) Brute Force**

* Try every pair (`i`, `j`) in the array.
* If `nums[i] + nums[j] == target`, return `[i, j]`.
* Easy to implement but inefficient.

**2) Hash Map (One-Pass)**

* Keep a hash map of value → index.
* For each number `x`, compute `complement = target − x`.
* If the complement is in the map, you found the solution.
* Efficient as only one pass gives output.

---

## Algorithm Descriptions

### Approach 1 — Brute Force (Naive)

Loop over all possible pairs (`i`, `j`), check if they sum to `target`.

**Pseudocode**

```
for i from 0 to n−1
  for j from i+1 to n−1
    if nums[i] + nums[j] == target
      return [i, j]
```

**Time Complexity:** O(n²)
**Space Complexity:** O(1) 

---

### Approach 2 — Hash Map (Optimal)

Traverse the list once.
For each number, check if its complement (target − current number) already exists in the hash map.
If it does, return indices. If not, store the current number in the map.

**Pseudocode**

```
let map = empty dictionary
for i from 0 to n−1
  complement = target − nums[i]
  if complement in map
    return [map[complement], i]
  map[nums[i]] = i
```

**Time Complexity:** O(n)
**Space Complexity:** O(n) 

---

## Code Implementations

### Java

```java
import java.util.HashMap;

public class TwoSum {
    public static int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{-1, -1}; // guaranteed one solution exists
    }
}
```

**Key Notes**

* Uses one hash map pass.
* Returns indices in arbitrary order.

---

### Swift

```swift
func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
    var map = [Int: Int]()
    
    for i in 0..<nums.count {
        let complement = target - nums[i]
        if let j = map[complement] {
            return [j, i]
        }
        map[nums[i]] = i
    }
    return []
}
```

**Key Notes**

* Dictionary lookup is average O(1).
* Stops early when match is found.

---

## Complexity Summary

| Approach            | Time  | Space |                    
| ------------------- | ----- | ----- | 
| Brute Force         | O(n²) | O(1)  |                    
| Hash Map (One-Pass) | O(n)  | O(n)  | 

---

## Best Approach

The **Hash Map (One-Pass)** is best:

* Takes linear time - so works better for higher contraints.
* Early exit as soon as complement is found.

(Brute Force is only useful as a starter or baseline explanation.)

---

## Final Comment

**Thought Style:**
Clarifying requirements: indices are required, not values, and exactly one solution exists. 

**Approach Choice:**
Try brute force first to understand the problem. Then think of optimization, in this case, hash map.

**Base Cases / Edge Cases:**

* Minimum length array of size 2 always has an answer per problem statement.
* Negative and positive values both allowed.
* Complement must refer to a different index.

**Optimal Solution:**
One-pass hash map is O(n) time and O(n) space. It finds the answer in a single linear scan, using constant-time dictionary operations. Return indices as soon as you detect the complement. 

---
