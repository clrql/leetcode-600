
  # linked-list-cycle-ii

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
    // Step 1: Check if the list has a cycle
    slow, fast := head, head
    hasCycle := false
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            hasCycle = true
            break
        }
    }
    
    // Step 2: Find the node where the cycle begins
    if hasCycle {
        slow = head
        for slow != fast {
            slow = slow.Next
            fast = fast.Next
        }
        return slow
    }
    
    // Step 3: No cycle found
    return nil
}
  ```
  