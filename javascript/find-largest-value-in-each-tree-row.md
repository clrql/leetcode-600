
  # find-largest-value-in-each-tree-row

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
 * @return {number[]}
 */
function largestValues(root) {
    if (!root) return [];
    
    const result = [];
    const queue = [root];
    
    while (queue.length) {
        let curr_level_size = queue.length;
        let max_val = Number.MIN_SAFE_INTEGER;
        
        for (let i = 0; i < curr_level_size; i++) {
            const node = queue.shift();
            max_val = Math.max(max_val, node.val);
            
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        
        result.push(max_val);
    }
    
    return result;
}
  ```
  