
  # remove-nth-node-from-end-of-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeNthFromEnd(head *ListNode, n int) *ListNode {
	// Create a dummy node as the previous node of the head
	dummy := &ListNode{Next: head}
	slow := dummy
	fast := dummy

	// Move the fast pointer n steps ahead
	for i := 0; i <= n; i++ {
		fast = fast.Next
	}

	// Move the slow and fast pointers simultaneously until the fast pointer reaches the end
	for fast != nil {
		slow = slow.Next
		fast = fast.Next
	}

	// Remove the nth node from the end by adjusting the pointers
	slow.Next = slow.Next.Next

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
  