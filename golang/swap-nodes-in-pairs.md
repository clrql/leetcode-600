
  # swap-nodes-in-pairs

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func swapPairs(head *ListNode) *ListNode {
	// If the list has fewer than two nodes or is empty, return the head
	if head == nil || head.Next == nil {
		return head
	}

	// Create a dummy node to serve as the new head
	dummy := &ListNode{Val: 0, Next: head.Next}
	prev := dummy

	// Swap nodes in pairs
	for head != nil && head.Next != nil {
		// Nodes to be swapped
		node1 := head
		node2 := head.Next

		// Swap nodes
		prev.Next = node2
		node1.Next = node2.Next
		node2.Next = node1

		// Move pointers forward
		prev = node1
		head = node1.Next
	}

	return dummy.Next
}
  ```
  