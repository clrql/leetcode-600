
  # build-array-where-you-can-find-the-maximum-exactly-k-comparisons

  ```c
  #define MOD 1000000007

int numOfArrays(int n, int m, int k) {
    int dp[n + 1][m + 1][k + 1];
    int prefix[n + 1][m + 1][k + 1];

    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            for (int l = 0; l <= k; l++) {
                dp[i][j][l] = 0;
                prefix[i][j][l] = 0;
            }
        }
    }

    for (int j = 1; j <= m; j++) {
        dp[1][j][1] = 1;
        prefix[1][j][1] = j;
    }

    for (int i = 2; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            for (int l = 1; l <= k; l++) {
                dp[i][j][l] = ((long long)j * dp[i - 1][j][l]) % MOD;

                if (j > 1 && l > 1) {
                    dp[i][j][l] = (dp[i][j][l] + prefix[i - 1][j - 1][l - 1]) % MOD;
                }

                prefix[i][j][l] = (prefix[i][j - 1][l] + dp[i][j][l]) % MOD;
            }
        }
    }

    return prefix[n][m][k];
}
  ```
  