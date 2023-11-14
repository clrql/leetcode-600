
  # divisor-game

  ```golang
  func divisorGame(n int) bool {
    dp := make([]bool, n+1)
    
    // Base case
    dp[1] = false
    
    for i := 2; i <= n; i++ {
        for x := 1; x < i; x++ {
            if i % x == 0 && !dp[i-x] {
                dp[i] = true
                break
            }
        }
    }
    
    return dp[n]
}

  ```
  