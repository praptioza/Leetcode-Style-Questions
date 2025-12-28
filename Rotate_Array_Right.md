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
* 1 <= nums.length <= 10^5
* -2^31 <= nums[i] <= 2^31 - 1
* 0 <= k <= 10^5

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

## High-Level Approaches Considered

**1) Brute Force**

* rotate for k times
* store the last element
* shift all elements to the right by 1
* place stored element at index 0
* repeat k times

Inefficient for large array size and large k

**2) Extra Array (Extra space)**

* Create a new array of the same size
* Place each element from the original array directly into its new position after rotation
* new index = (i + k) % n

Good if in-place is not required

**3) Reversal method (Optimal In-place Modification)**

* Reverse the whole array - reverse(arr, 0, n-1)
* Revrese the first k elements - reverse (arr, 0, k-1)
* Reverse the remaining n-k elements - reverse(arr, k, n-1)

or 
* Revrese the first k elements - reverse (arr, 0, k-1)
* Reverse the remaining n-k elements - reverse(arr, k, n-1)
* Reverse the whole array - reverse(arr, 0, n-1)

This is the most optimal solution as it does in-place rotation without using extra space and take O(N) time 
---


## Algorithm Descriptions

### Approach 1 — Brute Force (Naive)

Store last element, shift elements once, put last element on the first index. Repeat this k times

**Pseudocode**

```
repeat k times:
    last = arr[n-1]
    for i from n-1 to 1:
        arr[i] = arr[i-1]
    arr[0] = last
```

**Time Complexity: O(nk)** 
**Space Complexity: O(1)**   


### Approach 2 —  (using extra space)


**Pseudocode**

```
temp = array of size same as input
for i from 0 to n-1:
    newindex = (i + k) % n
    temp[newindex] = arr[i]
copy temp to arr
```

**Time Complexity: O(n)** 
**Space Complexity: O(n)** 

### Approach 3 - Reversal Method (Optimal in-place modification)

Reverse entire array, reverse first k elements, reverse remaining n-k elements

**Pseudocode**

```
reverse(arr, 0, n-1)
reverse(arr, 0, k-1)
reverse(arr, k, n-1)
```

**Time Complexity: O(n)** 
**Space Complexity: O(1)** 
---

## Code Implementations

### Java

**Approach 1: Brute force**
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n; 

        for(int i = 0; i < k; i++) {
            int last = nums[n-1];
            for(int j = n-1; j > 0; j--){
                nums[j] = nums[j-1];
            }
            nums[0] = last;
        }
    }
}
```

**Approach 2: Extra space solution**
```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        int temparr[] = new int[n];

        for(int i = 0; i < n; i++){
            temparr[(i+k)%n] = nums[i];
        }

        System.arraycopy(temparr, 0, nums, 0, n);
    }
}
```

**Approach 3: Optimal Reversal (in-plce)**
```java
class Solution {
    public void rotate(int[] nums, int k) {
        if(nums == null || nums.length == 0) { return; }  // check edge cases for null array to avoid testcase failure during runtime
        int n = nums.length;

        reverse(nums, 0, n-1);
        reverse(nums, 0, k-1);
        reverse(nums, k, n-1);
    }

    private void reverse(int[] nums, int left, int right) {
        while(left < right){
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
}
```

**Key Notes**

* Brute force is simple but inefficient for large input arrays and large k. 
* Reversal algorithm achieves optimal O(n) time with constant space as it is in-place array modification.
---

### Swift

**Approach 1: Brute force**
```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        let n = nums.count
        if n == 0 { return }

        for _ in 0..<k {
            let last = nums[n-1]
            for j in stride(from: n-1, to: 0, by: -1){
                nums[j] = nums[j-1]
            }
            nums[0] = last
        }
    }
}
```

**Approach 2: Extra space solution**
```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        let n = nums.count;
        if n == 0 { return }
        var temp = Array(repeating: 0, count: n)

        for i in 0..<n {
            temp[(i+k)%n] = nums[i]
        }
        nums = temp
    }
}
```

**Approach 3: Optimal Reversal (in-plce)**
```swift
class Solution {
    func rotate(_ nums: inout [Int], _ k: Int) {
        let n = nums.count; 
        if n == 0 { return }
        let k = k % n

        reverse(&nums, 0, n-1);
        reverse(&nums, 0, k-1);
        reverse(&nums, k, n-1);
     }

    private func reverse(_ nums : inout [Int], _ left: Int, _ right: Int){
        var l = left
        var r = right
        while l < r {
            nums.swapAt(l, r);
            l+=1;
            r-=1;
        }
   }
}
```
---

## Complexity Summary

| Approach                    | Time  | Space |                    
| --------------------------- | ----- | ----- | 
| Brute Force                 | O(nk) | O(1)  |                    
| Extra space                 | O(n)  | O(n)  | 
| Optimal Reversal (in-place) | O(n)  | O(n)  |

---

## Best Approach


The **Reversal Method (In-place)** is best:

* rotates array in linear time - so works better for higher contraints.
* In-place modification/reversal of array.

---

## Final Comment

**Thought Style:**
Clarifying requirements: Right rotation means elements from the end move to the front while maintaining the order

**Approach Choice:**
Try brute force first to understand the problem. Then think of optimization, in this case, reversal parts of array to simulate rotation

**Base Cases / Edge Cases:**

* for nums.length == 0 -> no rotation needed
* nums.length == 1 -> rotation has no effect
* k == 0 -> array remains same
* k >= nums.length -> reduce to k % n
* arrays with duplicate or negative values - rotation logic remains unaffected

**Optimal Solution:**
The reversal based approach is optimal for this problem. It:
* rotates the array in-place
* runs in O(n) time
* uses O(1) space

By reversing the entire array, then reversing first 'k' elements and the remaining elements seperately, required output rotated array can be obtained.

---
