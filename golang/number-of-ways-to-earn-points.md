
  # number-of-ways-to-earn-points

  ```golang
  func waysToReachTarget(target int, types [][]int) int {
    const mod = 1e9 + 7
    n := len(types)
    dp := make([]int, target+1)
    dp[0] = 1
    for i := 0; i < n; i++ {
        count, marks := types[i][0], types[i][1]
        for j := target; j >= marks; j-- {
            for k := 1; k <= count && j-k*marks >= 0; k++ {
                dp[j] = (dp[j] + dp[j-k*marks]) % mod
            }
        }
    }
    return dp[target]
}

  ```
  