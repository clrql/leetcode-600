
  # binary-tree-postorder-traversal

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func postorderTraversal(root *TreeNode) []int {
	if root == nil {
		return nil
	}

	var result []int
	stack := []*TreeNode{root}

	for len(stack) > 0 {
		node := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		// Insert node's value at the beginning of the result slice
		result = append([]int{node.Val}, result...)

		// Push left child first so that right child is processed first
		if node.Left != nil {
			stack = append(stack, node.Left)
		}

		// Push right child
		if node.Right != nil {
			stack = append(stack, node.Right)
		}
	}

	return result
}

/*
In this implementation, the postorderTraversal function takes a pointer to the root of the binary tree and returns a slice containing the postorder traversal of the tree. It initializes an empty result slice and a stack to store the nodes. It starts with the root node and pushes it onto the stack. Then, it enters a loop where it pops a node from the stack, inserts its value at the beginning of the result slice, and pushes its left and right children onto the stack (right child first to ensure left child is processed first in postorder traversal). The loop continues until the stack is empty. Finally, it returns the result slice containing the postorder traversal. The main function demonstrates several test cases and prints the respective postorder traversals of the binary trees.
*/
  ```
  