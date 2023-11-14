
  # increasing-order-search-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
var newRoot, current *TreeNode

func increasingBST(root *TreeNode) *TreeNode {
    newRoot = nil
    current = nil
    inOrderTraversal(root)
    return newRoot
}

func inOrderTraversal(node *TreeNode) {
    if node == nil {
        return
    }
    
    inOrderTraversal(node.Left)
    
    // Create a new node with the same value and set it as the right child
    newNode := &TreeNode{Val: node.Val}
    if newRoot == nil {
        newRoot = newNode
        current = newNode
    } else {
        current.Right = newNode
        current = newNode
    }
    
    inOrderTraversal(node.Right)
}
  ```
  