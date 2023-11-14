
  # palindrome-linked-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func isPalindrome(head *ListNode) bool {
    // Check if the list is empty or contains only one element
    if head == nil || head.Next == nil {
        return true
    }
    
    // Find the middle of the list
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    
    // Reverse the second half of the list
    prev := (*ListNode)(nil)
    curr := slow
    for curr != nil {
        next := curr.Next
        curr.Next = prev
        prev = curr
        curr = next
    }
    
    // Compare the first half with the reversed second half
    p1, p2 := head, prev
    for p2 != nil {
        if p1.Val != p2.Val {
            return false
        }
        p1 = p1.Next
        p2 = p2.Next
    }
    
    return true
}
  ```
  