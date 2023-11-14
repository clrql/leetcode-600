
  # binary-tree-inorder-traversal

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func inorderTraversal(root *TreeNode) []int {
	if root == nil {
		return []int{}
	}

	stack := []*TreeNode{}
	result := []int{}
	curr := root

	for curr != nil || len(stack) > 0 {
		// Traverse left subtree
		for curr != nil {
			stack = append(stack, curr)
			curr = curr.Left
		}

		// Visit the current node
		curr = stack[len(stack)-1]
		stack = stack[:len(stack)-1]
		result = append(result, curr.Val)

		// Traverse right subtree
		curr = curr.Right
	}

	return result
}
  ```
  