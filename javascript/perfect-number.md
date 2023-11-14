
  # perfect-number

  ```javascript
  /**
 * @param {number} num
 * @return {boolean}
 */
var checkPerfectNumber = function(num) {
  if (num <= 1) {
    return false;
  }

  var sum = 1;
  var sqrt = Math.floor(Math.sqrt(num));

  for (var i = 2; i <= sqrt; i++) {
    if (num % i === 0) {
      sum += i;

      var complement = num / i;
      if (complement !== i) {
        sum += complement;
      }
    }
  }

  return sum === num;
};

  ```
  