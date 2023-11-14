
  # complement-of-base-10-integer

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var bitwiseComplement = function(n) {
  var mask = (1 << n.toString(2).length) - 1;
  return n ^ mask;
};
  ```
  