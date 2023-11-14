
  # construct-string-from-binary-tree

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
 * @return {string}
 */
var tree2str = function(root) {
  if (root === null) {
    return '';
  }
  
  // Recursive function to construct the string
  function constructString(node) {
    let str = node.val.toString();
    
    if (node.left !== null) {
      str += '(' + constructString(node.left) + ')';
    } else if (node.right !== null) {
      str += '()';
    }
    
    if (node.right !== null) {
      str += '(' + constructString(node.right) + ')';
    }
    
    return str;
  }
  
  return constructString(root);
};

  ```
  