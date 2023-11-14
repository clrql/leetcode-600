
  # subtree-of-another-tree

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
 * @param {TreeNode} subRoot
 * @return {boolean}
 */
var isSubtree = function(s, t) {
  // Helper function to check if two trees are identical
  function isIdentical(tree1, tree2) {
    if (tree1 === null && tree2 === null) {
      return true;
    }
    if (tree1 === null || tree2 === null) {
      return false;
    }
    return (
      tree1.val === tree2.val &&
      isIdentical(tree1.left, tree2.left) &&
      isIdentical(tree1.right, tree2.right)
    );
  }

  // Base case: If the main tree is null, return false
  if (s === null) {
    return false;
  }

  // Check if the current subtree is identical to the given subtree
  if (isIdentical(s, t)) {
    return true;
  }

  // Recursively check if the subtree exists in the left or right child of the main tree
  return isSubtree(s.left, t) || isSubtree(s.right, t);
};
  ```
  