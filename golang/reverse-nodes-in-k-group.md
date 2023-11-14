
  # reverse-nodes-in-k-group

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseKGroup(head *ListNode, k int) *ListNode {
	count := 0
	current := head

	// Count the number of nodes in the list
	for count < k && current != nil {
		current = current.Next
		count++
	}

	// If there are at least k nodes, reverse them
	if count == k {
		nextGroupHead := reverseKGroup(current, k) // Reverse the remaining groups recursively

		// Reverse the current group
		for count > 0 {
			next := head.Next
			head.Next = nextGroupHead
			nextGroupHead = head
			head = next
			count--
		}

		head = nextGroupHead
	}

	return head
}

func createLinkedList(arr []int) *ListNode {
	if len(arr) == 0 {
		return nil
	}

	head := &ListNode{
		Val: arr[0],
	}

	current := head
	for i := 1; i < len(arr); i++ {
		node := &ListNode{
			Val: arr[i],
		}
		current.Next = node
		current = current.Next
	}

	return head
}

func printLinkedList(head *ListNode) {
	current := head
	for current != nil {
		fmt.Print(current.Val, " ")
		current = current.Next
	}
	fmt.Println()
}
  ```
  