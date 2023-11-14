
  # remove-linked-list-elements

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeElements(head *ListNode, val int) *ListNode {
	dummy := &ListNode{Next: head}
	prev := dummy
	current := head

	for current != nil {
		if current.Val == val {
			prev.Next = current.Next
		} else {
			prev = current
		}
		current = current.Next
	}

	return dummy.Next
}

// Helper function to create a linked list from an array
func createLinkedList(arr []int) *ListNode {
	dummy := &ListNode{}
	current := dummy

	for _, val := range arr {
		current.Next = &ListNode{Val: val}
		current = current.Next
	}

	return dummy.Next
}

// Helper function to convert a linked list to a string
func linkedListToString(head *ListNode) string {
	result := ""
	current := head

	for current != nil {
		result += fmt.Sprintf("%d -> ", current.Val)
		current = current.Next
	}

	result += "nil"

	return result
}

/*
In this implementation, the removeElements function takes a pointer to the head of the linked list and an integer val to remove. It uses a dummy node and two pointers (prev and current) to iterate through the linked list. If the current node has a value equal to val, it bypasses the current node by updating the Next pointer of the previous node. Otherwise, it updates the prev pointer to the current node. Finally, it returns the Next pointer of the dummy node, which points to the modified head of the linked list.

The createLinkedList function is a helper function that takes an array of integers and creates a linked list. The linkedListToString function converts a linked list to a string representation for printing purposes.
*/
  ```
  