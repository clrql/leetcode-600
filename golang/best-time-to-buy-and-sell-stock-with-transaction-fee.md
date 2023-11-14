
  # best-time-to-buy-and-sell-stock-with-transaction-fee

  ```golang
  func maxProfit(prices []int, fee int) int {
    n := len(prices)
    if n <= 1 {
        return 0
    }
    
    // Initialize variables to track the maximum profit with and without stock
    cash := 0
    hold := -prices[0]
    
    // Iterate through the prices and update the variables
    for i := 1; i < n; i++ {
        prevCash := cash
        cash = max(cash, hold+prices[i]-fee)
        hold = max(hold, prevCash-prices[i])
    }
    
    // Return the maximum profit without stock (cash)
    return cash
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  