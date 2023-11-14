
  # interleaving-string

  ```javascript
  /**
 * @param {string} s1
 * @param {string} s2
 * @param {string} s3
 * @return {boolean}
 */
var isInterleave = function(s1, s2, s3) {
  const m = s1.length;
  const n = s2.length;

  if (m + n !== s3.length) {
    return false;
  }

  const dp = new Array(m + 1).fill(false).map(() => new Array(n + 1).fill(false));

  dp[0][0] = true;

  // Check for s1 prefix
  for (let i = 1; i <= m; i++) {
    if (s1[i - 1] === s3[i - 1] && dp[i - 1][0]) {
      dp[i][0] = true;
    }
  }

  // Check for s2 prefix
  for (let j = 1; j <= n; j++) {
    if (s2[j - 1] === s3[j - 1] && dp[0][j - 1]) {
      dp[0][j] = true;
    }
  }

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      const k = i + j - 1;
      if (
        (s1[i - 1] === s3[k] && dp[i - 1][j]) ||
        (s2[j - 1] === s3[k] && dp[i][j - 1])
      ) {
        dp[i][j] = true;
      }
    }
  }

  return dp[m][n];
}
  ```
  