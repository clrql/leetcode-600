
  # maximum-twin-sum-of-a-linked-list

  ```golang
  /**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func pairSum(head *ListNode) int {
    var stack []int = []int{}
    var answer int
    var first int

    // create two pointers
    fast, slow := head, head 

    for nil != fast {
        //while we have fast pointer, add slow pointer value to stack
        stack = append(stack, slow.Val)

        //update slow and fast pointers
        slow = slow.Next
        fast = fast.Next.Next
    }

    for nil != slow {
        // while we have slow pointer, we pop value from stack
        first, stack = stack[len(stack) - 1], stack[:len(stack) - 1]
        // and if our sum of popped value and slow pointer value greater than ans, update ans
        if slow.Val + first > answer {
            answer = slow.Val + first
        }

        // update slow pointer
        slow = slow.Next 
    }

    

    return answer
}

  ```
  