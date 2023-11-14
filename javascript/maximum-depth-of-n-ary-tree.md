
  # maximum-depth-of-n-ary-tree

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
 * @return {number}
 */
var maxDepth = function(root) {
    if (root === null) {
        return 0;
    }

    let max = 0;
    
    for (let child of root.children) {
        const depth = maxDepth(child);
        if (depth > max) {
            max = depth;
        }
    }

    return max + 1;
};
  ```
  