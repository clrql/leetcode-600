
  # path-sum-iii

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func pathSum(root *TreeNode, targetSum int) int {
    if root == nil {
        return 0
    }
    
    return countPaths(root, targetSum) + pathSum(root.Left, targetSum) + pathSum(root.Right, targetSum)
}

func countPaths(node *TreeNode, targetSum int) int {
    if node == nil {
        return 0
    }
    
    count := 0
    if node.Val == targetSum {
        count++
    }
    
    count += countPaths(node.Left, targetSum-node.Val)
    count += countPaths(node.Right, targetSum-node.Val)
    
    return count
}
  ```
  