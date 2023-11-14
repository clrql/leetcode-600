
  # sort-list

  ```javascript
  /**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
function mergeSort(head) {
  // Base case: empty list or single node
  if (!head || !head.next) {
    return head;
  }

  // Split the list into two halves
  let mid = findMiddle(head);
  let left = head;
  let right = mid.next;
  mid.next = null;

  // Recursively sort the two halves
  let sortedLeft = mergeSort(left);
  let sortedRight = mergeSort(right);

  // Merge the sorted halves
  return merge(sortedLeft, sortedRight);
}

function findMiddle(head) {
  let slow = head;
  let fast = head;

  while (fast.next && fast.next.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow;
}

function merge(left, right) {
  let dummy = new ListNode(0);
  let curr = dummy;

  while (left && right) {
    if (left.val < right.val) {
      curr.next = left;
      left = left.next;
    } else {
      curr.next = right;
      right = right.next;
    }
    curr = curr.next;
  }

  if (left) {
    curr.next = left;
  } else if (right) {
    curr.next = right;
  }

  return dummy.next;
}

var sortList = function(head) {
  return mergeSort(head);
};
  ```
  