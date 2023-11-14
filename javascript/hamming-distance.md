
  # hamming-distance

  ```javascript
  /**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
var hammingDistance = function(x, y) {
  var xorResult = x ^ y;
  var binaryString = xorResult.toString(2);
  var distance = 0;

  for (var i = 0; i < binaryString.length; i++) {
    if (binaryString[i] === '1') {
      distance++;
    }
  }

  return distance;
};
  ```
  