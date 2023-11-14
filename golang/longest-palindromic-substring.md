
  # longest-palindromic-substring

  ```golang
  func longestPalindrome(s string) string {
    n := len(s)
    dp := make([][]bool, n)
    for i := range dp {
        dp[i] = make([]bool, n)
    }

    var longestPal string
    for l := 0; l < n; l++ {
        for i := 0; i+l < n; i++ {
            j := i + l
            if l == 0 {
                dp[i][j] = true
            } else if l == 1 {
                dp[i][j] = s[i] == s[j]
            } else {
                dp[i][j] = s[i] == s[j] && dp[i+1][j-1]
            }

            if dp[i][j] && l+1 > len(longestPal) {
                longestPal = s[i : j+1]
            }
        }
    }

    return longestPal
}
  ```
  