
  # best-time-to-buy-and-sell-stock-iv

  ```javascript
  /**
 * @param {number} k
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(k, prices) {
  const n = prices.length;
  
  // If k is greater than or equal to half the length of prices,
  // we can make as many transactions as we want, so we can use
  // a greedy approach to find the maximum profit.
  if (k >= Math.floor(n / 2)) {
    let maxProfit = 0;
    for (let i = 1; i < n; i++) {
      if (prices[i] > prices[i - 1]) {
        maxProfit += prices[i] - prices[i - 1];
      }
    }
    return maxProfit;
  }
  
  // Initialize the dp array
  const dp = new Array(n);
  for (let i = 0; i < n; i++) {
    dp[i] = new Array(k + 1).fill(0);
  }
  
  // Fill in the dp array
  for (let j = 1; j <= k; j++) {
    let maxDiff = -prices[0];
    for (let i = 1; i < n; i++) {
      dp[i][j] = Math.max(dp[i - 1][j], prices[i] + maxDiff);
      maxDiff = Math.max(maxDiff, dp[i - 1][j - 1] - prices[i]);
    }
  }
  
  return dp[n - 1][k];
}

  ```
  