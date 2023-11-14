
  # lowest-common-ancestor-of-a-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
    // Base case: if the root is nil or matches either of the given nodes, return the root
    if root == nil || root == p || root == q {
        return root
    }

    // Recursively find the lowest common ancestor in the left and right subtrees
    left := lowestCommonAncestor(root.Left, p, q)
    right := lowestCommonAncestor(root.Right, p, q)

    // If both left and right subtrees return a non-nil value, it means p and q are in different subtrees,
    // so the current root is the lowest common ancestor
    if left != nil && right != nil {
        return root
    }

    // If only the left subtree returns a non-nil value, it means both p and q are in the left subtree
    // and the lowest common ancestor is in the left subtree as well
    if left != nil {
        return left
    }

    // If only the right subtree returns a non-nil value, it means both p and q are in the right subtree
    // and the lowest common ancestor is in the right subtree as well
    if right != nil {
        return right
    }

    // If both left and right subtrees return nil, it means p and q are not found in the current subtree
    // Return nil in this case
    return nil
}

  ```
  