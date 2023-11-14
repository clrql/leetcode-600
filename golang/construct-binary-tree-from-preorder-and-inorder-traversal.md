
  # construct-binary-tree-from-preorder-and-inorder-traversal

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
	if len(preorder) == 0 {
		return nil
	}

	// The first element in the preorder traversal is the root of the tree
	rootVal := preorder[0]
	root := &TreeNode{Val: rootVal}

	// Find the root index in the inorder traversal
	var rootIndex int
	for i, val := range inorder {
		if val == rootVal {
			rootIndex = i
			break
		}
	}

	// Split the inorder traversal into left and right subtrees
	leftInorder := inorder[:rootIndex]
	rightInorder := inorder[rootIndex+1:]

	// Split the preorder traversal into left and right subtrees
	leftPreorder := preorder[1 : len(leftInorder)+1]
	rightPreorder := preorder[len(leftInorder)+1:]

	// Recursively build the left and right subtrees
	root.Left = buildTree(leftPreorder, leftInorder)
	root.Right = buildTree(rightPreorder, rightInorder)

	return root
}
  ```
  