
  # detect-capital

  ```javascript
  /**
 * @param {string} word
 * @return {boolean}
 */
var detectCapitalUse = function(word) {
  var uppercaseCount = 0;
  var lowercaseCount = 0;

  for (var i = 0; i < word.length; i++) {
    if (word[i] === word[i].toUpperCase()) {
      uppercaseCount++;
    } else {
      lowercaseCount++;
    }
  }

  if (uppercaseCount === word.length || lowercaseCount === word.length) {
    return true;
  }

  if (uppercaseCount === 1 && word[0] === word[0].toUpperCase()) {
    return true;
  }

  return false;
};

  ```
  