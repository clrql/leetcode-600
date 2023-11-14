
  # linked-list-cycle

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

function hasCycle(head: ListNode | null): boolean {
    if (head === null || head.next === null) {
        return false; // No cycle if there are less than 2 nodes
    }
    
    let tortoise = head;
    let hare = head;
    
    while (hare !== null && hare.next !== null) {
        tortoise = tortoise.next;
        hare = hare.next.next;
        
        if (tortoise === hare) {
            return true; // Cycle detected
        }
    }
    
    return false; // No cycle found
}

  ```
  