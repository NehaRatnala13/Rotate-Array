# Rotate-Array
Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.
# LeetCode 189: Rotate Array

## Problem Description
Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

### Example 1
* **Input:** `nums = [1,2,3,4,5,6,7]`, `k = 3`
* **Output:** `[5,6,7,1,2,3,4]`
* **Explanation:**
  * Rotate 1 steps to the right: `[7,1,2,3,4,5,6]`
  * Rotate 2 steps to the right: `[6,7,1,2,3,4,5]`
  * Rotate 3 steps to the right: `[5,6,7,1,2,3,4]`

## Solution: The Reversal Algorithm (Optimal)
The most optimal solution modifies the array **in-place** with **O(1) extra space** using a three-step array reversal technique.

### Algorithm Steps
1. **Normalize k:** If k is greater than the array length (n), rotating by k is equivalent to rotating by `k % n`.
2. **Reverse the entire array:** This puts the elements destined for the front at the beginning, but in reverse order.
3. **Reverse the first k elements:** Corrects the order of the newly rotated elements.
4. **Reverse the remaining n-k elements:** Corrects the order of the rest of the array.

### Complexity Analysis
* **Time Complexity:** **O(n)** – The algorithm passes over the array elements a constant number of times.
* **Space Complexity:** **O(1)** – No extra memory or auxiliary data structures are used.

## Python 3 Source Code

```python
from typing import List

class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n  # Handle cases where k is greater than array length
        
        # Helper function to reverse a slice of the array in-place
        def reverse(start: int, end: int) -> None:
            while start < end:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
                end -= 1
        
        # Step 1: Reverse the whole array
        reverse(0, n - 1)
        # Step 2: Reverse the first k elements
        reverse(0, k - 1)
        # Step 3: Reverse the remaining elements
        reverse(k, n - 1)

# --- Main Execution Block for Testing ---
if __name__ == "__main__":
    solution = Solution()
    
    # Test Case 1
    test_nums1 = [1, 2, 3, 4, 5, 6, 7]
    k1 = 3
    print(f"Original 1: {test_nums1}, k = {k1}")
    solution.rotate(test_nums1, k1)
    print(f"Rotated 1:  {test_nums1}\n")
    
    # Test Case 2
    test_nums2 = [-1, -100, 3, 99]
    k2 = 2
    print(f"Original 2: {test_nums2}, k = {k2}")
    solution.rotate(test_nums2, k2)
    print(f"Rotated 2:  {test_nums2}")
```
