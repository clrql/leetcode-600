
  # reverse-string-ii

  ```javascript
  /**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function(s, k) {
  var chars = s.split('');

  for (var i = 0; i < chars.length; i += 2 * k) {
    var left = i;
    var right = Math.min(i + k - 1, chars.length - 1);

    while (left < right) {
      var temp = chars[left];
      chars[left] = chars[right];
      chars[right] = temp;

      left++;
      right--;
    }
  }

  return chars.join('');
};

  ```
  