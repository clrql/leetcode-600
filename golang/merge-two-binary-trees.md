
  # merge-two-binary-trees

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func mergeTrees(root1 *TreeNode, root2 *TreeNode) *TreeNode {
    // Base cases
    if root1 == nil {
        return root2
    }
    if root2 == nil {
        return root1
    }

    // Merge the current nodes
    merged := &TreeNode{
        Val:   root1.Val + root2.Val,
        Left:  mergeTrees(root1.Left, root2.Left),
        Right: mergeTrees(root1.Right, root2.Right),
    }

    return merged
}

  ```
  