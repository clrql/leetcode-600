
  # reverse-linked-list-ii

  ```typescript
  /**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseBetween(head: ListNode | null, left: number, right: number): ListNode | null {
    if (!head || left === right) {
        return head;
    }
    
    // Create a dummy node to handle cases where left = 1
    const dummy = new ListNode(0);
    dummy.next = head;
    
    // Find the node at position (left - 1)
    let preLeft: ListNode | null = dummy;
    for (let i = 1; i < left; i++) {
        preLeft = preLeft!.next;
    }
    
    // Reverse the sublist from left to right
    let prev: ListNode | null = null;
    let curr: ListNode | null = preLeft!.next;
    for (let i = left; i <= right; i++) {
        const next = curr!.next;
        curr!.next = prev;
        prev = curr;
        curr = next;
    }
    
    // Connect the reversed sublist back to the original list
    preLeft!.next.next = curr;
    preLeft!.next = prev;
    
    return dummy.next;
}

  ```
  