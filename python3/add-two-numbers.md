
  # add-two-numbers

  ```python3
  # Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        current = dummy
        carry = 0

        p = l1
        q = l2

        while p is not None or q is not None:
            x = p.val if p else 0
            y = q.val if q else 0

            total = x + y + carry
            carry = total // 10

            current.next = ListNode(total % 10)
            current = current.next

            if p:
                p = p.next
            if q:
                q = q.next

        if carry > 0:
            current.next = ListNode(carry)

        return dummy.next
  ```
  