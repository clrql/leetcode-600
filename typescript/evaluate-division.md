
  # evaluate-division

  ```typescript
  function calcEquation(
  equations: string[][],
  values: number[],
  queries: string[][]
): number[] {
  const graph = new Map<string, Map<string, number>>();

  // Build the graph with variable pairs and values
  for (let i = 0; i < equations.length; i++) {
    const [a, b] = equations[i];
    const value = values[i];

    if (!graph.has(a)) {
      graph.set(a, new Map<string, number>());
    }
    if (!graph.has(b)) {
      graph.set(b, new Map<string, number>());
    }

    graph.get(a)!.set(b, value);
    graph.get(b)!.set(a, 1 / value);
  }

  // Evaluate queries using DFS
  const results: number[] = [];
  for (const [c, d] of queries) {
    if (!graph.has(c) || !graph.has(d)) {
      results.push(-1.0); // At least one variable is missing
    } else {
      results.push(dfs(c, d, new Set<string>()));
    }
  }

  return results;

  function dfs(a: string, b: string, visited: Set<string>): number {
    if (a === b) {
      return 1.0; // Found the target variable
    }

    visited.add(a);

    for (const [neighbor, value] of graph.get(a)!.entries()) {
      if (!visited.has(neighbor)) {
        const result = dfs(neighbor, b, visited);
        if (result !== -1.0) {
          return value * result;
        }
      }
    }

    return -1.0; // Cannot find a path to the target variable
  }
}

  ```
  