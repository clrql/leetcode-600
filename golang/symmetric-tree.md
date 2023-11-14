
  # symmetric-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSymmetric(root *TreeNode) bool {
    // Recursive approach
    return isMirror(root, root)
    
    // Iterative approach
    // if root == nil {
    //     return true
    // }
    // queue := []*TreeNode{root.Left, root.Right}
    // for len(queue) > 0 {
    //     left := queue[0]
    //     right := queue[1]
    //     queue = queue[2:]
    //     if left == nil && right == nil {
    //         continue
    //     }
    //     if left == nil || right == nil || left.Val != right.Val {
    //         return false
    //     }
    //     queue = append(queue, left.Left, right.Right, left.Right, right.Left)
    // }
    // return true
}

func isMirror(left *TreeNode, right *TreeNode) bool {
    if left == nil && right == nil {
        return true
    }
    if left == nil || right == nil || left.Val != right.Val {
        return false
    }
    return isMirror(left.Left, right.Right) && isMirror(left.Right, right.Left)
}
  ```
  