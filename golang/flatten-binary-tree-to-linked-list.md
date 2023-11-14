
  # flatten-binary-tree-to-linked-list

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func flatten(root *TreeNode) {
	if root == nil || (root.Left == nil && root.Right == nil) {
		return
	}

	if root.Left != nil {
		flatten(root.Left)

		temp := root.Right
		root.Right = root.Left
		root.Left = nil

		curr := root.Right
		for curr.Right != nil {
			curr = curr.Right
		}

		curr.Right = temp
	}

	flatten(root.Right)
}
  ```
  