
  # longest-zigzag-path-in-a-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func longestZigZag(root *TreeNode) int {
    if root == nil {
        return 0
    }
    
    maxLen := 0
    dfs(root.Left, 1, 0, &maxLen)
    dfs(root.Right, 1, 1, &maxLen)
    
    return maxLen
}

func dfs(node *TreeNode, length, direction int, maxLen *int) {
    if node == nil {
        return
    }
    
    *maxLen = max(*maxLen, length)
    
    if direction == 0 {
        dfs(node.Left, 1, 0, maxLen)
        dfs(node.Right, length+1, 1, maxLen)
    } else {
        dfs(node.Right, 1, 1, maxLen)
        dfs(node.Left, length+1, 0, maxLen)
    }
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
  ```
  