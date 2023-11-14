
  # add-two-numbers-ii

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    // Reverse the input lists
    l1 = reverseList(l1)
    l2 = reverseList(l2)
    
    // Initialize variables
    var head *ListNode
    carry := 0
    
    // Iterate through the lists and add the corresponding digits
    for l1 != nil || l2 != nil || carry != 0 {
        sum := carry
        
        if l1 != nil {
            sum += l1.Val
            l1 = l1.Next
        }
        
        if l2 != nil {
            sum += l2.Val
            l2 = l2.Next
        }
        
        digit := sum % 10
        carry = sum / 10
        
        // Create a new node with the calculated digit
        newNode := &ListNode{Val: digit, Next: head}
        head = newNode
    }
    
    return head
}

// Helper function to reverse a linked list
func reverseList(head *ListNode) *ListNode {
    var prev *ListNode
    
    for head != nil {
        next := head.Next
        head.Next = prev
        prev = head
        head = next
    }
    
    return prev
}
  ```
  