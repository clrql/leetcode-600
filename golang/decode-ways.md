
  # decode-ways

  ```golang
  func numDecodings(s string) int {
    n := len(s)
    if n == 0 {
        return 0
    }

    // Create a DP array to store the number of ways to decode up to i-th character
    dp := make([]int, n+1)
    dp[0] = 1
    if s[0] != '0' {
        dp[1] = 1
    } else {
        return 0
    }

    for i := 2; i <= n; i++ {
        oneDigit, _ := strconv.Atoi(s[i-1 : i])
        twoDigits, _ := strconv.Atoi(s[i-2 : i])

        if oneDigit >= 1 {
            dp[i] += dp[i-1]
        }
        if twoDigits >= 10 && twoDigits <= 26 {
            dp[i] += dp[i-2]
        }
    }

    return dp[n]
}

  ```
  