
  # construct-quad-tree

  ```golang
  
func construct(grid [][]int) *Node {
    n := len(grid)
    return buildQuadTree(grid, 0, 0, n)
}

func buildQuadTree(grid [][]int, x, y, size int) *Node {
    if size == 1 {
        return &Node{
            Val:       grid[x][y] == 1,
            IsLeaf:    true,
            TopLeft:   nil,
            TopRight:  nil,
            BottomLeft: nil,
            BottomRight: nil,
        }
    }
    
    halfSize := size / 2
    topLeft := buildQuadTree(grid, x, y, halfSize)
    topRight := buildQuadTree(grid, x, y+halfSize, halfSize)
    bottomLeft := buildQuadTree(grid, x+halfSize, y, halfSize)
    bottomRight := buildQuadTree(grid, x+halfSize, y+halfSize, halfSize)
    
    if isLeafNode(topLeft) && isLeafNode(topRight) && isLeafNode(bottomLeft) && isLeafNode(bottomRight) &&
        topLeft.Val == topRight.Val && topRight.Val == bottomLeft.Val && bottomLeft.Val == bottomRight.Val {
        return &Node{
            Val:       topLeft.Val,
            IsLeaf:    true,
            TopLeft:   nil,
            TopRight:  nil,
            BottomLeft: nil,
            BottomRight: nil,
        }
    }
    
    return &Node{
        Val:       false,
        IsLeaf:    false,
        TopLeft:   topLeft,
        TopRight:  topRight,
        BottomLeft: bottomLeft,
        BottomRight: bottomRight,
    }
}

func isLeafNode(node *Node) bool {
    return node != nil && node.IsLeaf
}
  ```
  