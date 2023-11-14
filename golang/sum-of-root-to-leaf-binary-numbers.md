
  # sum-of-root-to-leaf-binary-numbers

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumRootToLeaf(root *TreeNode) int {
    return sumRootToLeafHelper(root, 0)
}

func sumRootToLeafHelper(node *TreeNode, currentSum int) int {
    if node == nil {
        return 0
    }

    // Update the current binary number by left-shifting and adding the current node's value.
    currentSum = (currentSum << 1) + node.Val

    // If it's a leaf node, return the binary number.
    if node.Left == nil && node.Right == nil {
        return currentSum
    }

    // Recursively compute the sum for left and right subtrees.
    leftSum := sumRootToLeafHelper(node.Left, currentSum)
    rightSum := sumRootToLeafHelper(node.Right, currentSum)

    return leftSum + rightSum
}
  ```
  