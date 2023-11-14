
  # sum-root-to-leaf-numbers

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumNumbers(root *TreeNode) int {
	if root == nil {
		return 0
	}
	return calculatePathSum(root, 0)
}

func calculatePathSum(node *TreeNode, currentSum int) int {
	if node == nil {
		return 0
	}

	currentSum = currentSum*10 + node.Val

	if node.Left == nil && node.Right == nil {
		return currentSum
	}

	return calculatePathSum(node.Left, currentSum) + calculatePathSum(node.Right, currentSum)
}
  ```
  