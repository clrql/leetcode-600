
  # word-pattern

  ```javascript
  /**
 * @param {string} pattern
 * @param {string} s
 * @return {boolean}
 */
var wordPattern = function(pattern, s) {
  const words = s.split(' ');

  if (pattern.length !== words.length) {
    return false;
  }

  const patternToWord = new Map();
  const wordToPattern = new Map();

  for (let i = 0; i < pattern.length; i++) {
    const char = pattern[i];
    const word = words[i];

    if (!patternToWord.has(char) && !wordToPattern.has(word)) {
      patternToWord.set(char, word);
      wordToPattern.set(word, char);
    } else if (patternToWord.get(char) !== word || wordToPattern.get(word) !== char) {
      return false;
    }
  }

  return true;
}
  ```
  