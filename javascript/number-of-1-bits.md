
  # number-of-1-bits

  ```javascript
  /**
 * @param {number} n - a positive integer
 * @return {number}
 */
var hammingWeight = function(n) {
    return Number(n).toString(2).replaceAll("0", "").length
};
  ```
  