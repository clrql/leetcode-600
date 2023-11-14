
  # unique-paths-ii

  ```javascript
  /**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    const m = obstacleGrid.length;
    const n = obstacleGrid[0].length;

    if (obstacleGrid[0][0] === 1 || obstacleGrid[m - 1][n - 1] === 1) {
        return 0; // If the starting or ending position is an obstacle, there is no path
    }

    const dp = Array(m).fill(0).map(() => Array(n).fill(0));
    dp[0][0] = 1; // Set the starting position as reachable

    // Initialize the first column
    for (let i = 1; i < m; i++) {
        if (obstacleGrid[i][0] === 0) {
            dp[i][0] = dp[i - 1][0];
        }
    }

    // Initialize the first row
    for (let j = 1; j < n; j++) {
        if (obstacleGrid[0][j] === 0) {
            dp[0][j] = dp[0][j - 1];
        }
    }

    // Calculate the number of paths for each cell
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (obstacleGrid[i][j] === 0) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }

    return dp[m - 1][n - 1]; // Return the number of paths for the bottom-right cell
}
  ```
  