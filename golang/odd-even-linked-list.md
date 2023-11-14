
  # odd-even-linked-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func oddEvenList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    
    oddHead := head
    evenHead := head.Next
    odd := oddHead
    even := evenHead
    
    for even != nil && even.Next != nil {
        odd.Next = even.Next
        odd = odd.Next
        even.Next = odd.Next
        even = even.Next
    }
    
    odd.Next = evenHead
    
    return oddHead

}
  ```
  