
  # construct-binary-tree-from-inorder-and-postorder-traversal

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(inorder []int, postorder []int) *TreeNode {
    if len(inorder) == 0 {
        return nil
    }

    // Create a map to store the indices of inorder elements
    indexMap := make(map[int]int)
    for i, val := range inorder {
        indexMap[val] = i
    }

    return buildTreeHelper(inorder, postorder, 0, len(inorder)-1, 0, len(postorder)-1, indexMap)
}

func buildTreeHelper(inorder []int, postorder []int, inStart, inEnd, postStart, postEnd int, indexMap map[int]int) *TreeNode {
    if inStart > inEnd || postStart > postEnd {
        return nil
    }

    // The last element in postorder is the root of the current subtree
    rootVal := postorder[postEnd]
    root := &TreeNode{Val: rootVal}

    // Find the index of the root value in inorder
    rootIndex := indexMap[rootVal]

    // Calculate the number of nodes in the left subtree
    leftSubtreeSize := rootIndex - inStart

    // Recursively build the left and right subtrees
    root.Left = buildTreeHelper(inorder, postorder, inStart, rootIndex-1, postStart, postStart+leftSubtreeSize-1, indexMap)
    root.Right = buildTreeHelper(inorder, postorder, rootIndex+1, inEnd, postStart+leftSubtreeSize, postEnd-1, indexMap)

    return root
}
  ```
  