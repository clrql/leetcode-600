
  # edit-distance

  ```golang
  func minDistance(word1 string, word2 string) int {
    m, n := len(word1), len(word2)

    // Create a 2D array to store the minimum operations
    dp := make([][]int, m+1)
    for i := range dp {
        dp[i] = make([]int, n+1)
    }

    // Initialize the first row and column of the dp array
    for i := 0; i <= m; i++ {
        dp[i][0] = i
    }
    for j := 0; j <= n; j++ {
        dp[0][j] = j
    }

    // Fill in the dp array
    for i := 1; i <= m; i++ {
        for j := 1; j <= n; j++ {
            if word1[i-1] == word2[j-1] {
                dp[i][j] = dp[i-1][j-1] // Characters match, no operation needed
            } else {
                dp[i][j] = 1 + min(min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1])
                // 1 + minimum of (insertion, deletion, substitution)
            }
        }
    }

    return dp[m][n]
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
  ```
  