
  # k-th-symbol-in-grammar

  ```javascript
  /**
 * @param {number} n
 * @param {number} k
 * @return {number}
 */
var kthGrammar = function(n, k) {
    if (n === 1) {
        return 0;
    }
    
    // Calculate the mid point of the previous row.
    const mid = Math.pow(2, n - 1) / 2;
    
    // If k is in the first half of the row, it will have the same value as kthGrammar(n - 1, k).
    if (k <= mid) {
        return kthGrammar(n - 1, k);
    }
    // If k is in the second half, it will have the opposite value of k - mid in the previous row.
    return 1 - kthGrammar(n - 1, k - mid);
};
  ```
  