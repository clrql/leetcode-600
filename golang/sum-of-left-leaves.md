
  # sum-of-left-leaves

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumOfLeftLeaves(root *TreeNode) int {
	if root == nil {
		return 0
	}

	sum := 0

	// Check if the left child is a left leaf
	if root.Left != nil && root.Left.Left == nil && root.Left.Right == nil {
		sum += root.Left.Val
	}

	// Recursively calculate the sum of left leaves in the left and right subtrees
	sum += sumOfLeftLeaves(root.Left)
	sum += sumOfLeftLeaves(root.Right)

	return sum
}

/*
In this implementation, the sumOfLeftLeaves function takes the root of a binary tree and calculates the sum of all left leaves in the tree.

We start with a base case where if the root is nil, we return 0. Then, we initialize a variable sum to 0.

To calculate the sum of left leaves, we check if the left child of the current node is a left leaf. We can determine this by checking if the left child exists (root.Left != nil) and if it has no children (root.Left.Left == nil && root.Left.Right == nil). If it satisfies both conditions, we add the value of the left child to the sum.

Next, we recursively call sumOfLeftLeaves on the left and right subtrees to calculate the sum of left leaves in those subtrees. We add the returned values to the sum.

Finally, we return the sum as the result.
*/
  ```
  