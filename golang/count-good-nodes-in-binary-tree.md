
  # count-good-nodes-in-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func goodNodes(root *TreeNode) int {
    return countGoodNodes(root, root.Val)
}

func countGoodNodes(node *TreeNode, maxValue int) int {
    if node == nil {
        return 0
    }
    
    count := 0
    if node.Val >= maxValue {
        count = 1
        maxValue = node.Val
    }
    
    count += countGoodNodes(node.Left, maxValue)
    count += countGoodNodes(node.Right, maxValue)
    
    return count
}
  ```
  