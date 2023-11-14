
  # factorial-trailing-zeroes

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var trailingZeroes = function(n) {
  let count = 0;
  
  // Count the number of multiples of 5 in the factorial
  while (n >= 5) {
    count += Math.floor(n / 5);
    n = Math.floor(n / 5);
  }
  
  return count;
};
  ```
  