
  # construct-the-rectangle

  ```javascript
  /**
 * @param {number} area
 * @return {number[]}
 */
var constructRectangle = function(area) {
  var sqrt = Math.floor(Math.sqrt(area));

  for (var i = sqrt; i >= 1; i--) {
    if (area % i === 0) {
      return [area / i, i];
    }
  }
};

  ```
  