
  # binary-tree-preorder-traversal

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func preorderTraversal(root *TreeNode) []int {
	if root == nil {
		return nil
	}

	var result []int
	stack := []*TreeNode{root}

	for len(stack) > 0 {
		node := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		result = append(result, node.Val)

		// Push right child first so that left child is processed first
		if node.Right != nil {
			stack = append(stack, node.Right)
		}

		// Push left child
		if node.Left != nil {
			stack = append(stack, node.Left)
		}
	}

	return result
}
  ```
  