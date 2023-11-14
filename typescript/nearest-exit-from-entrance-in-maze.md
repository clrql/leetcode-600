
  # nearest-exit-from-entrance-in-maze

  ```typescript
  function nearestExit(maze: string[][], entrance: number[]): number {
  const rows = maze.length;
  const cols = maze[0].length;
  const directions = [[-1, 0], [1, 0], [0, -1], [0, 1]];
  const queue: number[][] = [entrance];
  const visited: boolean[][] = [];

  for (let i = 0; i < rows; i++) {
    visited[i] = [];
    for (let j = 0; j < cols; j++) {
      visited[i][j] = false;
    }
  }

  visited[entrance[0]][entrance[1]] = true;
  let steps = 0;

  while (queue.length > 0) {
    const size = queue.length;

    for (let i = 0; i < size; i++) {
      const [x, y] = queue.shift()!;

      if (isExit(x, y, rows, cols)) {
        if (!(x === entrance[0] && y === entrance[1])) {
          return steps;
        }
      }

      for (const [dx, dy] of directions) {
        const nx = x + dx;
        const ny = y + dy;

        if (isValid(nx, ny, rows, cols, maze, visited)) {
          queue.push([nx, ny]);
          visited[nx][ny] = true;
        }
      }
    }

    steps++;
  }

  return -1;
}

function isValid(
  x: number,
  y: number,
  rows: number,
  cols: number,
  maze: string[][],
  visited: boolean[][]
): boolean {
  return (
    x >= 0 &&
    x < rows &&
    y >= 0 &&
    y < cols &&
    maze[x][y] === "." &&
    !visited[x][y]
  );
}

function isExit(x: number, y: number, rows: number, cols: number): boolean {
  return (
    x === 0 || x === rows - 1 || y === 0 || y === cols - 1
  );
}

  ```
  