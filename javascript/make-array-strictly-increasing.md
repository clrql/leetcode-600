
  # make-array-strictly-increasing

  ```javascript
  /**
 * @param {number[]} arr1
 * @param {number[]} arr2
 * @return {number}
 */
var makeArrayIncreasing = function(a, b) {
    // insert -1 as first, insert Infinity as last
    a.unshift(-1), a.push(Infinity)
    
    // ascending
    b = Array.from(new Set(b)).sort((a, b) => a - b)

    // as count
    let n = a.length
    
    // set dp according to count
    let dp = new Array(n).fill(Infinity)
    
    // first 0
    dp[0] = 0
    
    // compare from 1
    for (let i = 1; i < n; i++) {
        let j = search(a[i]);

        for (let k = 1; k <= Math.min(i-1, j); k++) {
            if (a[i-k-1] < b[j - k]) {
                dp[i] = Math.min(dp[i], dp[i-k-1] + k);
            }
        }

        if (a[i-1] < a[i]) {
            dp[i] = Math.min(dp[i], dp[i-1])
        }
    }

    // finite as -1
    return isFinite(dp[n -1]) ? dp[n - 1] : -1

    // find 
    function search(v) {
        // set left and right for compare
        let ans = 0, max = b.length - 1

        // loop
        while(ans <= max) {
            // set middle of
            let m = ans + ((max - ans) >> 1)
            // according to condition
            b[m] < v ? (ans = m + 1) : (max = m - 1)
        }

        // result
        return ans
    }
}
  ```
  