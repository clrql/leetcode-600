
  # univalued-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isUnivalTree(root *TreeNode) bool {
    return isUnivalTreeHelper(root, root.Val)
}

func isUnivalTreeHelper(node *TreeNode, val int) bool {
    if node == nil {
        return true
    }

    if node.Val != val {
        return false
    }

    return isUnivalTreeHelper(node.Left, val) && isUnivalTreeHelper(node.Right, val)
}
  ```
  