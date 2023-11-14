
  # second-minimum-node-in-a-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findSecondMinimumValue(root *TreeNode) int {
    min1 := root.Val
    min2 := math.MaxInt64

    dfs(root, min1, &min2)

    if min2 == math.MaxInt64 {
        return -1
    }

    return min2
}

func dfs(node *TreeNode, min1 int, min2 *int) {
    if node == nil {
        return
    }

    if node.Val > min1 && node.Val <= *min2 {
        *min2 = node.Val
    }

    dfs(node.Left, min1, min2)
    dfs(node.Right, min1, min2)
}

  ```
  