
  # base-7

  ```javascript
  /**
 * @param {number} num
 * @return {string}
 */
var convertToBase7 = function(num) {
    if (num === 0) return '0';
    let res = '';
    let neg = num < 0;
    num = Math.abs(num);
    while (num > 0) {
        let rem = num % 7;
        res = rem.toString() + res;
        num = Math.floor(num/7);
    }
    return neg ? '-'+res : res;
};
  ```
  