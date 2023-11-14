
  # design-graph-with-shortest-path-calculator

  ```golang
  type Graph struct {
	nodes  int
	adj    map[int]map[int]int
	edges  [][]int
}

func Constructor(n int, edges [][]int) Graph {
	graph := Graph{
		nodes: n,
		adj:   make(map[int]map[int]int),
		edges: edges,
	}

	for _, edge := range edges {
		from, to, cost := edge[0], edge[1], edge[2]
		if _, ok := graph.adj[from]; !ok {
			graph.adj[from] = make(map[int]int)
		}
		graph.adj[from][to] = cost
	}

	return graph
}

func (g *Graph) AddEdge(edge []int) {
	from, to, cost := edge[0], edge[1], edge[2]
	if _, ok := g.adj[from]; !ok {
		g.adj[from] = make(map[int]int)
	}
	g.adj[from][to] = cost
	g.edges = append(g.edges, edge)
}

func (g *Graph) ShortestPath(node1 int, node2 int) int {
	visited := make(map[int]bool)
	distances := make(map[int]int)

	for i := 0; i < g.nodes; i++ {
		distances[i] = math.MaxInt32
	}
	distances[node1] = 0

	for i := 0; i < g.nodes-1; i++ {
		minNode := -1
		minDistance := math.MaxInt32

		for j := 0; j < g.nodes; j++ {
			if !visited[j] && distances[j] < minDistance {
				minNode = j
				minDistance = distances[j]
			}
		}

		visited[minNode] = true

		for to, cost := range g.adj[minNode] {
			if distances[minNode]+cost < distances[to] {
				distances[to] = distances[minNode] + cost
			}
		}
	}

	if distances[node2] == math.MaxInt32 {
		return -1
	}

	return distances[node2]
}

/**
 * Your Graph object will be instantiated and called as such:
 * obj := Constructor(n, edges);
 * obj.AddEdge(edge);
 * param_2 := obj.ShortestPath(node1,node2);
 */
  ```
  