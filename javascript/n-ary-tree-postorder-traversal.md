
  # n-ary-tree-postorder-traversal

  ```javascript
  /**
 * // Definition for a Node.
 * function Node(val,children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {Node|null} root
 * @return {number[]}
 */
var postorder = function(root) {
    if (root === null) {
      return [];
    }

    const stack = [root];
    const result = [];

    while (stack.length > 0) {
      const node = stack.pop();
      result.unshift(node.val);
      for (let child of node.children) {
        stack.push(child);
      }
    }

    return result;
};
  ```
  