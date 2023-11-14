
  # binary-trees-with-factors

  ```javascript
  /**
 * @param {number[]} arr
 * @return {number}
 */
var numFactoredBinaryTrees = function(arr) {
    const MOD = 1e9 + 7;
    arr.sort((a, b) => a - b); // Sort the array in ascending order
    const n = arr.length;
    const dp = new Array(n).fill(1); // Initialize a DP array with 1 for each element
    
    const index = new Map(); // Create a map for easy access to array indices
    for (let i = 0; i < n; i++) {
        index.set(arr[i], i);
    }

    for (let i = 0; i < n; i++) {
        for (let j = 0; j < i; j++) {
            if (arr[i] % arr[j] === 0) {
                const factor = arr[i] / arr[j];
                if (index.has(factor)) {
                    const k = index.get(factor);
                    dp[i] = (dp[i] + dp[j] * dp[k]) % MOD;
                }
            }
        }
    }

    let total = 0;
    for (let i = 0; i < n; i++) {
        total = (total + dp[i]) % MOD;
    }
    
    return total;
};
  ```
  