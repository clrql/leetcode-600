
  # reorder-routes-to-make-all-paths-lead-to-the-city-zero

  ```typescript
  function minReorder(n: number, connections: number[][]): number {
  const graph = new Map<number, number[]>();
  const visited = new Set<number>();
  let changes = 0;

  for (const [from, to] of connections) {
    if (!graph.has(from)) {
      graph.set(from, []);
    }
    if (!graph.has(to)) {
      graph.set(to, []);
    }

    graph.get(from)!.push(to);
    graph.get(to)!.push(-from); // Mark reverse connections with negative sign
  }

  dfs(0); // Start DFS from city 0

  function dfs(city: number): void {
    visited.add(city);

    for (const neighbor of graph.get(city)!) {
      if (!visited.has(Math.abs(neighbor))) {
        changes += neighbor > 0 ? 1 : 0; // Increase changes count if the connection is reversed
        dfs(Math.abs(neighbor));
      }
    }
  }

  return changes;
}

  ```
  