
  # invert-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
	if root == nil {
		return nil
	}

	// Invert the left and right subtrees recursively
	root.Left, root.Right = invertTree(root.Right), invertTree(root.Left)

	return root
}
  ```
  