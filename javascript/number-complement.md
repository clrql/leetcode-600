
  # number-complement

  ```javascript
  /**
 * @param {number} num
 * @return {number}
 */
var findComplement = function(num) {
  var mask = (1 << num.toString(2).length) - 1;
  return num ^ mask;
};
  ```
  