
  # two-sum-iv-input-is-a-bst

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findTarget(root *TreeNode, k int) bool {
    // Create an empty hash set
    numSet := make(map[int]bool)
    return dfs(root, k, numSet)
}

func dfs(node *TreeNode, k int, numSet map[int]bool) bool {
    if node == nil {
        return false
    }

    // Check if the complement exists in the hash set
    if numSet[k-node.Val] {
        return true
    }

    // Add the current node's value to the hash set
    numSet[node.Val] = true

    // Recursively search the left and right subtrees
    return dfs(node.Left, k, numSet) || dfs(node.Right, k, numSet)
}
  ```
  