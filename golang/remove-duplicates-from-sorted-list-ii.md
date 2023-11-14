
  # remove-duplicates-from-sorted-list-ii

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteDuplicates(head *ListNode) *ListNode {
	// Create a dummy node as the previous node of the head
	dummy := &ListNode{Next: head}
	prev := dummy
	current := head

	for current != nil {
		// Skip all duplicate nodes
		for current.Next != nil && current.Val == current.Next.Val {
			current = current.Next
		}

		// If no duplicates, update the prev and current pointers
		if prev.Next == current {
			prev = prev.Next
		} else {
			prev.Next = current.Next
		}

		current = current.Next
	}

	return dummy.Next
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
  