
  # binary-tree-paths

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func binaryTreePaths(root *TreeNode) []string {
	if root == nil {
		return nil
	}

	var paths []string
	dfs(root, "", &paths)
	return paths
}

func dfs(node *TreeNode, path string, paths *[]string) {
	if node.Left == nil && node.Right == nil {
		// Reached a leaf node, append the path to the result
		*paths = append(*paths, path+strconv.Itoa(node.Val))
		return
	}

	// Append the current node's value to the path
	path += strconv.Itoa(node.Val) + "->"

	if node.Left != nil {
		dfs(node.Left, path, paths)
	}

	if node.Right != nil {
		dfs(node.Right, path, paths)
	}
}

/*
In this implementation, the binaryTreePaths function takes a pointer to the root of the binary tree and returns a slice of strings representing all root-to-leaf paths.

The dfs function performs a depth-first search starting from the given node. It takes the current node, the current path string, and a pointer to the result slice of paths. If the current node is a leaf node (no left or right children), it appends the current node's value to the path and adds the path to the result slice. If the current node has a left child, it recursively calls dfs on the left child, passing the updated path. Similarly, if the current node has a right child, it recursively calls dfs on the right child, passing the updated path.
*/
  ```
  