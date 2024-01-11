# 19. Remove Nth Node From End of List
Given the head of a linked list, remove the nth node from the end of the list and return its head.

 

Example 1:


Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Example 2:

Input: head = [1], n = 1
Output: []
Example 3:

Input: head = [1,2], n = 1
Output: [1]
 

Constraints:

The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
 

Follow up: Could you do this in one pass?

## Solution
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        fast = head
        slow = head

        # Find the nth position in the linkedlist
        for i in range(n):
          fast = fast.next
        
        # now that fast is in the nth position that means the gap between fast and slow is n, now iterate fast until the end of the linked list, that way the slow node is now the nth position from the end
        if not fast:
          return head.next
        
        while fast.next:
          slow = slow.next
          fast = fast.next
        
        slow.next = slow.next.next
        return head

```