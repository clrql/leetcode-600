
  # delete-the-middle-node-of-a-linked-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteMiddle(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return nil
    }
    
    slow := head
    fast := head
    var prev *ListNode
    
    for fast != nil && fast.Next != nil {
        prev = slow
        slow = slow.Next
        fast = fast.Next.Next
    }
    
    prev.Next = slow.Next
    
    return head
}
  ```
  