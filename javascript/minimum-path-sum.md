
  # minimum-path-sum

  ```javascript
  /**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
  const m = grid.length;
  const n = grid[0].length;

  // Create a 2D array to store the minimum path sum
  const dp = new Array(m);
  for (let i = 0; i < m; i++) {
    dp[i] = new Array(n);
  }

  // Initialize the first cell
  dp[0][0] = grid[0][0];

  // Initialize the first column
  for (let i = 1; i < m; i++) {
    dp[i][0] = dp[i - 1][0] + grid[i][0];
  }

  // Initialize the first row
  for (let j = 1; j < n; j++) {
    dp[0][j] = dp[0][j - 1] + grid[0][j];
  }

  // Calculate the minimum path sum for each cell
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
    }
  }

  // Return the minimum path sum for the bottom-right cell
  return dp[m - 1][n - 1];
}
  ```
  