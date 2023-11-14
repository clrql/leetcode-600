
  # binary-tree-tilt

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
var findTilt = function(root) {
    let totalTilt = 0;

    function calculateTiltAndSum(node) {
        if (node === null) {
            return 0;
        }

        const leftSum = calculateTiltAndSum(node.left);
        const rightSum = calculateTiltAndSum(node.right);

        const tilt = Math.abs(leftSum - rightSum);

        totalTilt += tilt;

        return node.val + leftSum + rightSum;
    }

    calculateTiltAndSum(root);

    return totalTilt;
};
  ```
  