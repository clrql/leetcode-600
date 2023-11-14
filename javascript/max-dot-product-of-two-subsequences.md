
  # max-dot-product-of-two-subsequences

  ```javascript
  /**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
function maxDotProduct(nums1, nums2) {
  const m = nums1.length;
  const n = nums2.length;

  // Create a 2D array dp to store the maximum dot product at each (i, j) position.
  const dp = new Array(m + 1).fill(0).map(() => new Array(n + 1).fill(-Infinity));

  // Initialize the base cases.
  for (let i = 0; i <= m; i++) {
    for (let j = 0; j <= n; j++) {
      if (i === 0 || j === 0) {
        dp[i][j] = -Infinity;
      }
    }
  }

  // Fill in the dp array using dynamic programming.
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      dp[i][j] = Math.max(
        nums1[i - 1] * nums2[j - 1], // Include the current elements in the product
        dp[i - 1][j - 1] + nums1[i - 1] * nums2[j - 1], // Extend the previous subsequence
        dp[i - 1][j], // Skip the current element in nums2
        dp[i][j - 1] // Skip the current element in nums1
      );
    }
  }

  // The maximum dot product will be at dp[m][n].
  return dp[m][n];
}
  ```
  