
  # leaf-similar-trees

  ```typescript
  /**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function leafSimilar(root1: TreeNode | null, root2: TreeNode | null): boolean {
  const leaves1: number[] = [];
  const leaves2: number[] = [];

  getLeaves(root1, leaves1);
  getLeaves(root2, leaves2);

  if (leaves1.length !== leaves2.length) {
    return false;
  }

  for (let i = 0; i < leaves1.length; i++) {
    if (leaves1[i] !== leaves2[i]) {
      return false;
    }
  }

  return true;
}

function getLeaves(node: TreeNode | null, leaves: number[]): void {
  if (node === null) {
    return;
  }

  if (node.left === null && node.right === null) {
    leaves.push(node.val);
  }

  getLeaves(node.left, leaves);
  getLeaves(node.right, leaves);
}
  ```
  