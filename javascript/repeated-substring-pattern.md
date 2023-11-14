
  # repeated-substring-pattern

  ```javascript
  /**
 * @param {string} s
 * @return {boolean}
 */
var repeatedSubstringPattern = function(s) {
  var n = s.length;
  
  // Try all possible substrings
  for (var i = 1; i <= Math.floor(n / 2); i++) {
    if (n % i === 0) {
      var substring = s.slice(0, i);
      var repeatedSubstring = substring.repeat(n / i);
      
      if (repeatedSubstring === s) {
        return true;
      }
    }
  }
  
  return false;
};
  ```
  