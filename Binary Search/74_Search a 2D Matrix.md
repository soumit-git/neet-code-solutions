# 74. Search a 2D Matrix
You are given an m x n integer matrix matrix with the following two properties:

Each row is sorted in non-decreasing order.
The first integer of each row is greater than the last integer of the previous row.
Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in O(log(m * n)) time complexity.

 

Example 1:


Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
Example 2:


Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
 

Constraints:

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 100
- -104 <= matrix[i][j], target <= 104
## Solution
```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        lc, rc = 0, len(matrix) - 1
        while(lc <= rc):
          m = (lc + rc) // 2
          if matrix[m][-1] < target:
            lc = m + 1
          elif matrix[m][0] > target:
            rc = m - 1
          else:
            break
        if not (lc <= rc):
          return False
        
        l, r = 0, len(matrix[0]) - 1
        while (l <= r):
          mid = (l + r) // 2
          if matrix[m][mid] < target:
            l = mid + 1
          elif matrix[m][mid] > target:
            r = mid - 1
          else:
            return True
        
        return False
```