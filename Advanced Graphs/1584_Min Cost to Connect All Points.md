# 1584. Min Cost to Connect All Points
You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.

 

Example 1:


Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20
Explanation: 

We can connect the points as shown above to get the minimum cost of 20.
Notice that there is a unique path between every pair of points.
Example 2:

Input: points = [[3,12],[-2,5],[-4,1]]
Output: 18
 

Constraints:

1 <= points.length <= 1000
-106 <= xi, yi <= 106
All pairs (xi, yi) are distinct.

## Solution
```
class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        N = len(points)

        # Creating the adjacency list [cost, node]

        adj = { i:[] for i in range(N)}
        for i in range(N):
          x1, y1 = points[i]
          for j in range(i + 1, N):
            x2, y2 = points[j]
            dist = abs(x1 - x2) + abs(y1 - y2)
            adj[i].append([dist, j])
            adj[j].append([dist, i])
        
        # Prim's algorithm

        visit = set()
        res = 0
        minH = [[0, 0]]

        while len(visit) < N:
          cost, i = heapq.heappop(minH)
          if i in visit:
            continue
          res += cost
          visit.add(i)
          for neiCost, nei in adj[i]:
            if nei not in visit:
              heapq.heappush(minH, [neiCost, nei])
        
        return res
```