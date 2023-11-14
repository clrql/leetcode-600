
  # count-complete-tree-nodes

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func countNodes(root *TreeNode) int {
	if root == nil {
		return 0
	}

	leftHeight := getHeight(root.Left)
	rightHeight := getHeight(root.Right)

	if leftHeight == rightHeight {
		// The left subtree is a full binary tree of height leftHeight.
		// The total number of nodes in the left subtree can be calculated as 2^leftHeight - 1.
		return countNodes(root.Right) + (1 << leftHeight)
	} else {
		// The right subtree is a full binary tree of height rightHeight - 1.
		// The total number of nodes in the right subtree can be calculated as 2^(rightHeight-1) - 1.
		return countNodes(root.Left) + (1 << rightHeight)
	}
}

func getHeight(node *TreeNode) int {
	height := 0
	for node != nil {
		height++
		node = node.Left
	}
	return height
}
  ```
  