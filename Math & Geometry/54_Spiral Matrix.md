# 54. Spiral Matrix
Given an m x n matrix, return all elements of the matrix in spiral order.

 

Example 1:


Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
Example 2:


Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
 

Constraints:

m == matrix.length
n == matrix[i].length
1 <= m, n <= 10
-100 <= matrix[i][j] <= 100

## Solution
```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        l, r = 0, len(matrix[0])
        t, b = 0, len(matrix)

        while l < r and t < b:
          for i in range(l, r):
            res.append(matrix[t][i])
          t += 1

          for i in range(t, b):
            res.append(matrix[i][r - 1])
          r -= 1

          if not (l < r and t < b):
            break
          
          for i in range(r - 1, l - 1, -1):
            res.append(matrix[b - 1][i])
          b -= 1

          for i in range(b - 1, t - 1, -1):
            res.append(matrix[i][l])
          l += 1
        
        return res

```