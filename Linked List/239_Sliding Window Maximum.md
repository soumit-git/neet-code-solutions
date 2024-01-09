# 239. Sliding Window Maximum
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

 

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Example 2:

Input: nums = [1], k = 1
Output: [1]
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length

## Solution
```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        output = []
        l = r = 0
        q = deque()

        while r < len(nums):
          # remove smaller values from the queue
          while q and nums[q[-1]] < nums[r]:
            q.pop()
          # append the bigger value into the q
          q.append(r)
          # remove the left value from q
          if l > q[0]:
            q.popleft()
          
          # increase the left pointer when the window is larger than k
          if r + 1 >= k:
            output.append(nums[q[0]])
            l += 1
          r += 1
        
        return output
        
```