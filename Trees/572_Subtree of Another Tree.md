# 572. Subtree of Another Tree
Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

 

Example 1:


Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
Example 2:


Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
 

Constraints:

The number of nodes in the root tree is in the range [1, 2000].
The number of nodes in the subRoot tree is in the range [1, 1000].
-104 <= root.val <= 104
-104 <= subRoot.val <= 104
## Solution
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, s: Optional[TreeNode], t: Optional[TreeNode]) -> bool:
        if not t: return True
        if not s: return False

        if self.sameTree(s, t):
          return True
        
        return(self.isSubtree(s.left, t) or self.isSubtree(s.right, t))

      
    def sameTree(self, s, t):
      if not s and not t:
        return True
      if s and t and s.val == t.val:
        return(self.sameTree(s.left, t.left) and self.sameTree(s.right, t.right))
      return False
```