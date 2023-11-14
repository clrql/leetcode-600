
  # minimum-absolute-difference-in-bst

  ```javascript
  /**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val === undefined ? 0 : val);
 *     this.left = (left === undefined ? null : left);
 *     this.right = (right === undefined ? null : right);
 * }
 */

/**
 * @param {TreeNode} root
 * @return {number}
 */
var getMinimumDifference = function(root) {
  // Initialize variables
  var prev = null; // Previous node's value during traversal
  var minDiff = Infinity; // Minimum difference found
  
  // In-order traversal function
  function inorder(node) {
    if (node === null) return;
    
    // Traverse left subtree
    inorder(node.left);
    
    // Check difference with previous value
    if (prev !== null) {
      minDiff = Math.min(minDiff, node.val - prev);
    }
    
    // Update previous value
    prev = node.val;
    
    // Traverse right subtree
    inorder(node.right);
  }
  
  // Start traversal from the root
  inorder(root);
  
  // Return the minimum difference found
  return minDiff;
};

  ```
  