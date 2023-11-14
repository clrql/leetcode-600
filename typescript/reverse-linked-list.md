
  # reverse-linked-list

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

function reverseList(head: ListNode | null): ListNode | null {
    return reverseListRecursive(head)
};

function reverseListIterative(head: ListNode | null): ListNode | null {
  let prev: ListNode | null = null;
  let current: ListNode | null = head;

  while (current !== null) {
    const nextNode: ListNode | null = current.next;
    current.next = prev;
    prev = current;
    current = nextNode;
  }

  return prev;
}

function reverseListRecursive(head: ListNode | null): ListNode | null {
  if (head === null || head.next === null) {
    return head;
  }

  const reversedHead: ListNode | null = reverseListRecursive(head.next);
  head.next.next = head;
  head.next = null;

  return reversedHead;
}
  ```
  