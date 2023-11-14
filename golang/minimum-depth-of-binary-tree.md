
  # minimum-depth-of-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func minDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}

	if root.Left == nil && root.Right == nil {
		return 1
	}

	min := math.MaxInt32

	if root.Left != nil {
		min = getMin(min, minDepth(root.Left))
	}

	if root.Right != nil {
		min = getMin(min, minDepth(root.Right))
	}

	return min + 1
}

func getMin(a, b int) int {
	if a < b {
		return a
	}
	return b
}
  ```
  