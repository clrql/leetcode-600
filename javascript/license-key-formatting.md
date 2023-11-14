
  # license-key-formatting

  ```javascript
  /**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var licenseKeyFormatting = function(s, k) {
  // Remove dashes and convert to uppercase
  var formatted = s.replace(/-/g, '').toUpperCase();

  var result = [];
  var count = 0;

  // Iterate over the reversed string
  for (var i = formatted.length - 1; i >= 0; i--) {
    result.push(formatted[i]);
    count++;

    // Insert dashes every k characters
    if (count === k && i > 0) {
      result.push('-');
      count = 0;
    }
  }

  return result.reverse().join('');
};

  ```
  