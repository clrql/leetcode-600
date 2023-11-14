
  # maximum-level-sum-of-a-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxLevelSum(root *TreeNode) int {
	if root == nil {
		return 0
	}

	maxSum := math.MinInt64
	maxLevel := 0
	level := 1

	queue := []*TreeNode{root}

	for len(queue) > 0 {
		sum := 0
		size := len(queue)

		for i := 0; i < size; i++ {
			node := queue[0]
			queue = queue[1:]
			sum += node.Val

			if node.Left != nil {
				queue = append(queue, node.Left)
			}
			if node.Right != nil {
				queue = append(queue, node.Right)
			}
		}

		if sum > maxSum {
			maxSum = sum
			maxLevel = level
		}

		level++
	}

	return maxLevel
}
  ```
  