
  # diameter-of-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func diameterOfBinaryTree(root *TreeNode) int {
	if root == nil {
		return 0
	}

	diameter := 0
	calculateDiameter(root, &diameter)
	return diameter
}

func calculateDiameter(node *TreeNode, diameter *int) int {
	if node == nil {
		return 0
	}

	left := calculateDiameter(node.Left, diameter)
	right := calculateDiameter(node.Right, diameter)

	// Update the diameter if the current path is longer
	*diameter = int(math.Max(float64(*diameter), float64(left+right)))

	// Return the longest path from the current node
	return int(math.Max(float64(left), float64(right))) + 1
}
  ```
  