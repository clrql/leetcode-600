
  # binary-search-tree-iterator

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
type BSTIterator struct {
	stack []*TreeNode
}

func Constructor(root *TreeNode) BSTIterator {
	stack := make([]*TreeNode, 0)
	current := root

	for current != nil {
		stack = append(stack, current)
		current = current.Left
	}

	return BSTIterator{stack: stack}
}

func (it *BSTIterator) Next() int {
	node := it.stack[len(it.stack)-1]
	it.stack = it.stack[:len(it.stack)-1]

	current := node.Right
	for current != nil {
		it.stack = append(it.stack, current)
		current = current.Left
	}

	return node.Val
}

func (it *BSTIterator) HasNext() bool {
	return len(it.stack) > 0
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * obj := Constructor(root);
 * param_1 := obj.Next();
 * param_2 := obj.HasNext();
 */
  ```
  