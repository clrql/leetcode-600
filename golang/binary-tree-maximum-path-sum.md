
  # binary-tree-maximum-path-sum

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxPathSum(root *TreeNode) int {
	maxSum := math.MinInt32
	maxPathSumRecursive(root, &maxSum)
	return maxSum
}

func maxPathSumRecursive(node *TreeNode, maxSum *int) int {
	if node == nil {
		return 0
	}

	leftSum := max(maxPathSumRecursive(node.Left, maxSum), 0)
	rightSum := max(maxPathSumRecursive(node.Right, maxSum), 0)

	currentSum := node.Val + leftSum + rightSum
	*maxSum = max(*maxSum, currentSum)

	return node.Val + max(leftSum, rightSum)
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

  ```
  