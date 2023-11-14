
  # intersection-of-two-linked-lists

  ```javascript
  /**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} headA
 * @param {ListNode} headB
 * @return {ListNode}
 */
var getIntersectionNode = function(headA, headB) {
  let pA = headA;
  let pB = headB;

  while (pA !== pB) {
    pA = pA ? pA.next : headB; // Move pA to the head of headB if it reaches the end of headA
    pB = pB ? pB.next : headA; // Move pB to the head of headA if it reaches the end of headB
  }

  return pA; // Return the intersected node or null
};
  ```
  