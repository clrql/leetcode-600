
  # balanced-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isBalanced(root *TreeNode) bool {
	if root == nil {
		// An empty tree is considered balanced
		return true
	}

	// Check if the left and right subtrees are balanced
	leftHeight := getHeight(root.Left)
	rightHeight := getHeight(root.Right)
	heightDiff := math.Abs(float64(leftHeight - rightHeight))

	if heightDiff > 1 {
		// If the height difference is more than 1, the tree is not balanced
		return false
	}

	// Recursively check if both subtrees are balanced
	return isBalanced(root.Left) && isBalanced(root.Right)
}

func getHeight(node *TreeNode) int {
	if node == nil {
		// Base case: an empty subtree has height 0
		return 0
	}

	// Recursively compute the height of the left and right subtrees
	leftHeight := getHeight(node.Left)
	rightHeight := getHeight(node.Right)

	// The height of the current node is the maximum height of its subtrees plus 1
	return int(math.Max(float64(leftHeight), float64(rightHeight))) + 1
}

  ```
  