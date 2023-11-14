
  # number-of-provinces

  ```typescript
  function findCircleNum(isConnected: number[][]): number {
  const n = isConnected.length;
  const visited = new Array(n).fill(false);
  let provinces = 0;

  for (let i = 0; i < n; i++) {
    if (!visited[i]) {
      dfs(i);
      provinces++;
    }
  }

  function dfs(city: number): void {
    visited[city] = true;

    for (let j = 0; j < n; j++) {
      if (isConnected[city][j] === 1 && !visited[j]) {
        dfs(j);
      }
    }
  }

  return provinces;
}

  ```
  