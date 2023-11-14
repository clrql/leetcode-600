
  # best-time-to-buy-and-sell-stock

  ```javascript
  /**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let maxProfit = 0;
    let minPrice = prices[0];

    for (let i = 1; i < prices.length; i++) {
        // Update the minimum price if a lower price is found
        minPrice = Math.min(minPrice, prices[i]);

        // Calculate the potential profit if selling at the current price
        let profit = prices[i] - minPrice;

        // Update the maximum profit if a higher profit is found
        maxProfit = Math.max(maxProfit, profit);
    }

    return maxProfit;
}
  ```
  