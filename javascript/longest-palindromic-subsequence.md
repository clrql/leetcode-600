
  # longest-palindromic-subsequence

  ```javascript
  /**
 * @param {string} s
 * @return {number}
 */
var longestPalindromeSubseq = function(s) {
    const n = s.length;
    const dp = new Array(n).fill(0).map(() => new Array(n).fill(0));
    
    // Initialize diagonal elements to 1
    for (let i = 0; i < n; i++) {
        dp[i][i] = 1;
    }
    
    // Traverse array diagonally and fill in values
    for (let len = 2; len <= n; len++) {
        for (let i = 0; i <= n - len; i++) {
            const j = i + len - 1;
            if (s[i] === s[j]) {
                dp[i][j] = 2 + (len === 2 ? 0 : dp[i+1][j-1]);
            } else {
                dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
            }
        }
    }
    
    return dp[0][n-1];
};
  ```
  