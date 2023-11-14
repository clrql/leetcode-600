
  # reverse-integer

  ```javascript
  /**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let isnegative = x < 0;
    x = x.toString().replace("-", "");
    x = x.split("").reverse().join("").replace("^0+");
    x = parseInt(x) * (isnegative ? -1: 1);
    if (x > 2 ** 31 - 1 || x < -(2 ** 31)) return 0;
    return x;
};
  ```
  