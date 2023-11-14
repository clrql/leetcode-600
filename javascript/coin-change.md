
  # coin-change

  ```javascript
  /**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
var coinChange = function(coins, amount) {
  // Initialize a dp array with a length of amount + 1 and fill it with Infinity
  const dp = new Array(amount + 1).fill(Infinity);
  
  // The minimum number of coins needed to make amount 0 is 0
  dp[0] = 0;

  // Iterate through all amounts from 1 to amount
  for (let i = 1; i <= amount; i++) {
    // For each amount, try using each coin denomination
    for (let j = 0; j < coins.length; j++) {
      if (coins[j] <= i) {
        // If using the current coin leads to a smaller number of coins needed,
        // update the dp array with the new minimum number of coins
        dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
      }
    }
  }

  // If dp[amount] is still Infinity, it means the amount cannot be made up
  return dp[amount] === Infinity ? -1 : dp[amount];
}

  ```
  