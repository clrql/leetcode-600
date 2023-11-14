
  # rotate-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func rotateRight(head *ListNode, k int) *ListNode {
	// Check for empty list or k = 0
	if head == nil || k == 0 {
		return head
	}

	// Calculate the length of the list
	length := 1
	tail := head
	for tail.Next != nil {
		tail = tail.Next
		length++
	}

	// Calculate the actual rotation steps needed
	k = k % length
	if k == 0 {
		return head
	}

	// Find the new tail and new head
	newTail := head
	for i := 1; i < length-k; i++ {
		newTail = newTail.Next
	}
	newHead := newTail.Next

	// Perform the rotation
	newTail.Next = nil
	tail.Next = head

	return newHead
}
  ```
  