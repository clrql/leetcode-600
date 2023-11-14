
  # wildcard-matching

  ```golang
  func isMatch(s string, p string) bool {
    // Create a two-dimensional boolean array to store the matching results
    dp := make([][]bool, len(s)+1)
    for i := 0; i <= len(s); i++ {
        dp[i] = make([]bool, len(p)+1)
    }
    
    // An empty pattern matches an empty string
    dp[0][0] = true
    
    // Handling cases where '*' matches an empty sequence
    for j := 1; j <= len(p); j++ {
        if p[j-1] == '*' {
            dp[0][j] = dp[0][j-1]
        }
    }
    
    // Fill the dynamic programming table
    for i := 1; i <= len(s); i++ {
        for j := 1; j <= len(p); j++ {
            if p[j-1] == '*' {
                // Either '*' matches an empty sequence (dp[i][j-1]),
                // or '*' matches the current character in the string (dp[i-1][j]).
                dp[i][j] = dp[i][j-1] || dp[i-1][j]
            } else if p[j-1] == '?' || p[j-1] == s[i-1] {
                // If the current characters match or the pattern has a '?',
                // then the result depends on the previous characters' matching result.
                dp[i][j] = dp[i-1][j-1]
            }
        }
    }
    
    // The last cell of the table represents the matching result for the entire string and pattern
    return dp[len(s)][len(p)]
}

  ```
  