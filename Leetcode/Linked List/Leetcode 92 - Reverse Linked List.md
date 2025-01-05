- **Problem Link**: https://leetcode.com/problems/reverse-linked-list-ii/description/


## My Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def reverseBetween(self, head, left, right):
        # If the list is empty or left position is the same as right, return  
        # the original list
        if not head or left == right:
            return head

        # Create a dummy node to handle edge case when left = 1
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy

        # Move prev to the node just before the left position
        for _ in range(left - 1):
            prev = prev.next

        # Current node is the node at the left position
        curr = prev.next

        # Reverse the portion of the linked list between left and right 
        # positions
        for _ in range(right - left):
            next_node = curr.next
            curr.next = next_node.next
            next_node.next = prev.next
            prev.next = next_node

        # Return the updated head of the linked list
        return dummy.next
```

## Approach
- Advance one pointer to the left position 
- Reverse the portion in between the left and right position by either prepending to some dummy pointer or doing the fuckery in the code above
- Once you reach the "right" element, set the tail of the dummy list next pointer to the right's next pointer and the left's next pointer to the head of the dummy list


**Category**: Linked List


## Time and Space Complexity
- Time: O(n)
- Space: O(1)
## Similar Problems
- [[Leetcode]]