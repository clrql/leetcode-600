
  # same-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSameTree(p *TreeNode, q *TreeNode) bool {
    // If both trees are empty, they are considered the same
    if p == nil && q == nil {
        return true
    }
    
    // If one tree is empty and the other is not, they are not the same
    if p == nil || q == nil {
        return false
    }
    
    // If the values of the current nodes are different, they are not the same
    if p.Val != q.Val {
        return false
    }
    
    // Recursively check if the left and right subtrees are the same
    return isSameTree(p.Left, q.Left) && isSameTree(p.Right, q.Right)
}
  ```
  