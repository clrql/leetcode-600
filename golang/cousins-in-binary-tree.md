
  # cousins-in-binary-tree

  ```golang
  /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isCousins(root *TreeNode, x int, y int) bool {
    if root == nil {
        return false
    }

    queue := []struct {
        node   *TreeNode
        parent *TreeNode
        depth  int
    }{{root, nil, 0}}

    var parentX, parentY *TreeNode
    depthX, depthY := -1, -1

    for len(queue) > 0 {
        nodeInfo := queue[0]
        queue = queue[1:]
        node, parent, depth := nodeInfo.node, nodeInfo.parent, nodeInfo.depth

        if node.Val == x {
            parentX, depthX = parent, depth
        } else if node.Val == y {
            parentY, depthY = parent, depth
        }

        if parentX != nil && parentY != nil {
            break
        }

        if node.Left != nil {
            queue = append(queue, struct {
                node   *TreeNode
                parent *TreeNode
                depth  int
            }{node.Left, node, depth + 1})
        }
        if node.Right != nil {
            queue = append(queue, struct {
                node   *TreeNode
                parent *TreeNode
                depth  int
            }{node.Right, node, depth + 1})
        }
    }

    return depthX == depthY && parentX != parentY
}
  ```
  