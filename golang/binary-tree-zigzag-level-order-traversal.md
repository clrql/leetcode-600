
  # binary-tree-zigzag-level-order-traversal

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func zigzagLevelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{}
    }

    var result [][]int
    queue := []*TreeNode{root}
    level := 0

    for len(queue) > 0 {
        levelSize := len(queue)
        levelNodes := make([]int, levelSize)

        for i := 0; i < levelSize; i++ {
            node := queue[i]

            if level%2 == 0 {
                levelNodes[i] = node.Val
            } else {
                levelNodes[levelSize-i-1] = node.Val
            }

            if node.Left != nil {
                queue = append(queue, node.Left)
            }

            if node.Right != nil {
                queue = append(queue, node.Right)
            }
        }

        result = append(result, levelNodes)
        queue = queue[levelSize:]
        level++
    }

    return result
}
  ```
  