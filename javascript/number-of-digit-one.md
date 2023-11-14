
  # number-of-digit-one

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var countDigitOne = function(n) {
    let count = 0;
    for (let i = 1; i <= n; i *= 10) {
        const div = i * 10;
        count += Math.floor(n/div) * i + Math.min(Math.max(n % div - i + 1, 0), i)
    }
    return count
};
  ```
  