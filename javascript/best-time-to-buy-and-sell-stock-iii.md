
  # best-time-to-buy-and-sell-stock-iii

  ```javascript
  /**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  const n = prices.length;

  // Create two arrays to store the maximum profit for the first and second transactions
  const profits1 = new Array(n).fill(0);
  const profits2 = new Array(n).fill(0);

  let minPrice = prices[0];
  let maxProfit1 = 0;

  // Calculate the maximum profit for the first transaction
  for (let i = 1; i < n; i++) {
    minPrice = Math.min(minPrice, prices[i]);
    maxProfit1 = Math.max(maxProfit1, prices[i] - minPrice);
    profits1[i] = maxProfit1;
  }

  let maxPrice = prices[n - 1];
  let maxProfit2 = 0;
  let maxProfit = 0;

  // Calculate the maximum profit for the second transaction and overall maximum profit
  for (let i = n - 2; i >= 0; i--) {
    maxPrice = Math.max(maxPrice, prices[i]);
    maxProfit2 = Math.max(maxProfit2, maxPrice - prices[i]);
    profits2[i] = maxProfit2;
    maxProfit = Math.max(maxProfit, profits1[i] + profits2[i]);
  }

  return maxProfit;
}
  ```
  