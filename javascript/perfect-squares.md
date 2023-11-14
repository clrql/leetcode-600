
  # perfect-squares

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var numSquares = function(n) {
    // Create an array to store the minimum number of perfect squares for each value from 0 to n
    const dp = new Array(n + 1).fill(Number.MAX_SAFE_INTEGER);
  
    // Initialize the base case: 0 requires 0 perfect squares
    dp[0] = 0;
  
    // Iterate from 1 to n
    for (let i = 1; i <= n; i++) {
    // Iterate over all possible perfect squares less than or equal to i
        for (let j = 1; j * j <= i; j++) {
            // Calculate the minimum number of perfect squares for i
            dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
        }
    }
  
  // Return the result for n
  return dp[n];
};
  ```
  