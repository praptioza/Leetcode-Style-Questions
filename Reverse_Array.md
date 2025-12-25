# Reverse Array

## Problem Statement

Given an array of integers `nums`, **return the reverse of this array** such that it is an **in-place modification**.

### Example

```
Input: nums = [2,7,11,15]
Output: [15, 11, 7, 2]  
```

---

## Problem Understanding (in words)

Given a list of integers, reverse the list withount taking extra space.

---

---

## High-Level Approaches Considered

**1) Brute Force**

* Create another array of the same size.
* Copy the input array into the new array from the end.
* Takes extra space and inefficient if length of the array is too large

**2) Two-pointer swapping (One-Pass)**

* Keep a pointer 'i' at the starting index of the given input array
* Keep a pointer 'j' at the ending index of the given input array
* Swap the element at 'i' with the element at 'j'
* Efficient as only one pass gives output

---

## Algorithm Descriptions

### Approach 1 — Brute Force (Naive)

Loop over the input array from the end and copy each element to the newly created array

**Pseudocode**

```
create reversed_arr of size n

for i from 0 to n-1
    reversed_arr[n - 1 - i] = arr[i]

return reversed_arr
```

Time complexity: O(n)
Space Complexity: O(n)
This brute-force approach is not optimal because it uses extra space proportional to the input size.
---

### Approach 2 — Two-pointer In-place reversal (Optimal)

Take pointer 'i' (start index) and 'j' (end index) and swap the elements. Move 'i' and 'j' accordingly. This is called 'In-place modification' of the input array. This can be done in O(n) time and O(1) space. The algorithm pattern is called "Two pointer technique".

**Pseudocode**

```
i = 0, j = n-1
while i < j:
    temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
    i++
    j--
```

**Time Complexity:** O(n)
**Space Complexity:** O(1) 

---

---

## Code Implementations

### Java

```java

public class ReverseArray {
    public static int[] reverse(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
        return nums;
    }
}
```

**Key Notes**

* Uses one pass using two pointers and results in in-place reversal.

---

### Swift

Take pointer 'i' (start index) and 'j' (end index) and swap the elements. Move 'i' and 'j' accordingly.

In Swift, arrays are **value types**. So, passing them by value requires copying on mutation, which leads to O(n) extra space.

Using `inout` enables in-place modification with O(1) space. Without it, arrays are passed by value and parameters are immutable, so any mutation would only affect a local copy.

Note: `inout` allows the functio to modify the original array passed in. While calling the function, using & is mandatory for inout parameters as the array is passed by reference to allow modification.

```swift

Pass by value Solution:
```
func reverse(_ nums:[Int]) -> [Int] {
    var result = nums
    var left = 0
    var right = nums.count - 1
    
    while left < right {
        result.swapAt(left, right);
        left+=1
        right-=1
    }
    return result
}

var nums = [ 1,2, 3,4 ,5]
let reversed_nums = reverse(nums)
print(reversed_nums)
```

Pass by Reference Solution (Optimal)
```
func reverse(_ nums: inout[Int]) -> [Int] {
    var left = 0
    var right = nums.count - 1
    
    while left < right {
        nums.swapAt(left, right);
        left+=1
        right-=1
    }
    return nums
}

var nums = [ 1,2, 3,4 ,5]
let reversed_nums = reverse(&nums)
print(reversed_nums)
```

---

## Complexity Summary

| Approach               | Time  | Space |                    
| ---------------------- | ----- | ----- | 
| Brute Force            | O(n)  | O(n)  |                    
| Two-pointer (In-place) | O(n)  | O(1)  | 

---

## Best Approach

The **Two-pointer technique (One-Pass)** is best:

* Takes linear time - so works better for higher contraints.
* In-place modification/reversal of array.

---

## Final Comment

**Thought Style:**
Clarifying requirements: Reversing array is required, for supporting large input sizes, copying array to another array is not feasible.

**Approach Choice:**
Try brute force first to understand the problem. Then think of optimization, in this case, two-pointer.

**Base Cases / Edge Cases:**

* Empty array causes left < right condition to be false.
* Single element array causes left < right condition to be false.
* However, two pointer approach is iterative. So loop condition left < right implictly handles all base cases. So there is no need for :
```if nums.count <= 1 { return }```

**Optimal Solution:**
One-pass two-pointer technique is O(n) time and O(1) space. It finds the answer in a single linear scan, using constant-time operations and in-place reversal.

---
