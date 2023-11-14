
  # partition-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func partition(head *ListNode, x int) *ListNode {
	// Create two dummy nodes for the two partitions
	dummy1 := &ListNode{}
	dummy2 := &ListNode{}

	// Create two pointers for the current nodes in each partition
	curr1 := dummy1
	curr2 := dummy2

	// Traverse the original list
	for head != nil {
		// If the current node's value is less than x, add it to the first partition
		if head.Val < x {
			curr1.Next = head
			curr1 = curr1.Next
		} else { // If the current node's value is greater than or equal to x, add it to the second partition
			curr2.Next = head
			curr2 = curr2.Next
		}

		// Move to the next node in the original list
		head = head.Next
	}

	// Connect the two partitions
	curr1.Next = dummy2.Next
	curr2.Next = nil

	// Return the head of the first partition
	return dummy1.Next
}
  ```
  