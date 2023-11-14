
  # copy-list-with-random-pointer

  ```typescript
  /**
 * Definition for Node.
 * class Node {
 *     val: number
 *     next: Node | null
 *     random: Node | null
 *     constructor(val?: number, next?: Node, random?: Node) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *         this.random = (random===undefined ? null : random)
 *     }
 * }
 */

function copyRandomList(head: Node | null): Node | null {
  if (head === null) {
    return null;
  }

  const map: Map<Node, Node> = new Map();
  let current: Node | null = head;

  // Create new nodes with the same values
  while (current !== null) {
    const newNode = new Node(current.val);
    map.set(current, newNode);
    current = current.next;
  }

  current = head;

  // Set the next and random pointers of the new nodes
  while (current !== null) {
    const newNode = map.get(current)!;
    newNode.next = map.get(current.next) || null;
    newNode.random = map.get(current.random) || null;
    current = current.next;
  }

  return map.get(head)!;
}

  ```
  