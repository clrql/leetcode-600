
  # clone-graph

  ```golang
  /**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Neighbors []*Node
 * }
 */


func cloneGraph(node *Node) *Node {
    if node == nil {
        return nil
    }

    visited := make(map[*Node]*Node)
    return clone(node, visited)
}

func clone(node *Node, visited map[*Node]*Node) *Node {
    // If the node has already been visited, return the cloned node
    if visited[node] != nil {
        return visited[node]
    }

    // Create a new cloned node
    cloned := &Node{Val: node.Val, Neighbors: make([]*Node, len(node.Neighbors))}
    visited[node] = cloned

    // Clone the neighbors recursively
    for i, neighbor := range node.Neighbors {
        cloned.Neighbors[i] = clone(neighbor, visited)
    }

    return cloned
}
  ```
  