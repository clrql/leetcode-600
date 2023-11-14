
  # scramble-string

  ```golang
  func isScramble(s1 string, s2 string) bool {
    n := len(s1)
    if n != len(s2) {
        return false
    }

    // Initialize a 3D DP array to store the results
    dp := make([][][]bool, n)
    for i := range dp {
        dp[i] = make([][]bool, n)
        for j := range dp[i] {
            dp[i][j] = make([]bool, n+1)
        }
    }

    // Base case: strings of length 1
    for i := 0; i < n; i++ {
        for j := 0; j < n; j++ {
            if s1[i] == s2[j] {
                dp[i][j][1] = true
            }
        }
    }

    // Length of the substring to check
    for len := 2; len <= n; len++ {
        for i := 0; i <= n-len; i++ {
            for j := 0; j <= n-len; j++ {
                for k := 1; k < len; k++ {
                    // Check for unswapped and swapped substrings
                    if (dp[i][j][k] && dp[i+k][j+k][len-k]) || (dp[i][j+len-k][k] && dp[i+k][j][len-k]) {
                        dp[i][j][len] = true
                        break
                    }
                }
            }
        }
    }

    return dp[0][0][n]
}

  ```
  