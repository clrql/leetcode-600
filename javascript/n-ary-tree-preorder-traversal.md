
  # n-ary-tree-preorder-traversal

  ```javascript
  /**
 * // Definition for a Node.
 * function Node(val, children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {Node|null} root
 * @return {number[]}
 */
var preorder = function(root) {
  const result = [];
  
  // Recursive function to perform preorder traversal
  function traverse(node) {
    if (node === null) {
      return;
    }
    
    // Visit the current node
    result.push(node.val);
    
    // Traverse the children nodes recursively
    for (let child of node.children) {
      traverse(child);
    }
  }
  
  // Call the recursive function on the root node
  traverse(root);
  
  return result;
};

  ```
  