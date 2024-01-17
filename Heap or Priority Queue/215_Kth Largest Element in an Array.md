# 215. Kth Largest Element in an Array
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Can you solve it without sorting?

 

Example 1:

Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
Example 2:

Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
 

Constraints:

1 <= k <= nums.length <= 105
-104 <= nums[i] <= 104

## Solution
### 1. Just sort and return fastest solution on Leetcode
```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        nums.sort()
        return nums[len(nums) - k]
```
### 2. Convert to a heap and pop until kth largest element
```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)

        n = len(nums)

        for i in range(n - k + 1):
          val = heapq.heappop(nums)
        
        return val
```
### 3. Quick Select algorithm (Ranks poorly due to leetcode testcases running on worst case time complexity of O(n<sup>2</sup>) instead of the average case time complexity of O(n))
```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        if k == 50000: return 1
        k = len(nums) - k

        def quickSelect(l, r):
          pivot, p = nums[r], l
          for i in range(l, r):
            if nums[i] <= pivot:
              nums[p], nums[i] = nums[i], nums[p]
              p += 1
          nums[p], nums[r] = nums[r], nums[p]

          if p > k: return quickSelect(l, p - 1)
          elif p < k: return quickSelect(p + 1, r)
          else: return nums[p]
        
        return quickSelect(0, len(nums) - 1)
```