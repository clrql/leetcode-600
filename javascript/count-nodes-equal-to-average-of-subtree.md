
  # count-nodes-equal-to-average-of-subtree

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
 * @return {number}
 */
var averageOfSubtree = function(root) {
    // Helper function to calculate the sum and count of nodes in a subtree
    function calculateSubtreeAverage(node) {
        if (!node) {
            return [0, 0]; // [Sum, Count]
        }
        const [leftSum, leftCount] = calculateSubtreeAverage(node.left);
        const [rightSum, rightCount] = calculateSubtreeAverage(node.right);
        
        const subtreeSum = leftSum + rightSum + node.val;
        const subtreeCount = leftCount + rightCount + 1;
        
        if (node.val === Math.floor(subtreeSum / subtreeCount)) {
            result++;
        }
        
        return [subtreeSum, subtreeCount];
    }
    
    let result = 0;
    calculateSubtreeAverage(root);
    return result;
};
  ```
  