# 143. Reorder List
You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

 

Example 1:


Input: head = [1,2,3,4]
Output: [1,4,2,3]
Example 2:


Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
 

Constraints:

The number of nodes in the list is in the range [1, 5 * 104].
1 <= Node.val <= 1000
## Solution
### 1. Fast and Slow pointer approach (O(1) Memory)
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        slow, fast = head, head.next

        while fast and fast.next:
          slow = slow.next
          fast = fast.next.next
        
        second = slow.next
        prev = slow.next = None

        while second:
          tmp = second.next
          second.next = prev
          prev = second
          second = tmp
        
        first, second = head, prev
        while second:
          tmp1, tmp2 = first.next, second.next
          first.next = second
          second.next = tmp1
          first, second = tmp1, tmp2

```
### 2. Array approach (O(n) memory)
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        current = head
        nodes = []
        # traverse the linked list and append all the nodes into a list
        while current:
          nodes.append(current)
          current = current.next
        
        left, right = 0, len(nodes) - 1
        # use the two pointer approach to change the linking of the list
        while left < right:
          nodes[left].next = nodes[right]
          left += 1
          nodes[right].next = nodes[left]
          right -= 1
        
        nodes[left].next = None
```