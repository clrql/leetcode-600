
  # validate-binary-search-tree

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
 
function isValidBST(root: TreeNode | null): boolean {
  return validateNode(root, null, null);
}

function validateNode(node: TreeNode | null, min: number | null, max: number | null): boolean {
  if (node === null) {
    return true;
  }

  if ((min !== null && node.val <= min) || (max !== null && node.val >= max)) {
    return false;
  }

  return (
    validateNode(node.left, min, node.val) && 
    validateNode(node.right, node.val, max)
  );
}
  ```
  