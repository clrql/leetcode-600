
  # path-sum

  ```javascript
  /**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */

/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function(root, targetSum) {
  if (!root) {
    // If the root is null, there are no root-to-leaf paths
    return false;
  }

  if (!root.left && !root.right) {
    // If the current node is a leaf, check if its value equals the remaining target sum
    return root.val === targetSum;
  }

  // Recursively check if there is a path in the left or right subtree
  const remainingSum = targetSum - root.val;
  return (
    hasPathSum(root.left, remainingSum) ||
    hasPathSum(root.right, remainingSum)
  );
};

  ```
  