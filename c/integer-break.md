
  # integer-break

  ```c
  int integerBreak(int n) {
    if (n <= 3) {
        return n - 1;
    }

    int dp[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 3;

    for (int i = 4; i <= n; i++) {
        dp[i] = 0;
        for (int j = 1; j <= i / 2; j++) {
            int product = dp[j] * dp[i - j];
            if (product > dp[i]) {
                dp[i] = product;
            }
        }
    }

    return dp[n];
}

  ```
  