
  # maximal-square

  ```javascript
  /**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalSquare = function(matrix) {
  const rows = matrix.length;
  const cols = matrix[0].length;
  let maxSquareSize = 0;
  
  // Create a dynamic programming table
  const dp = new Array(rows + 1).fill(0).map(() => new Array(cols + 1).fill(0));
  
  // Iterate through the matrix
  for (let i = 1; i <= rows; i++) {
    for (let j = 1; j <= cols; j++) {
      if (matrix[i - 1][j - 1] === '1') {
        // Calculate the size of the square ending at (i, j)
        dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1;
        
        // Update the maximum square size
        maxSquareSize = Math.max(maxSquareSize, dp[i][j]);
      }
    }
  }
  
  // Return the area of the largest square
  return maxSquareSize * maxSquareSize;
}
  ```
  