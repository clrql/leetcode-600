
  # keyboard-row

  ```javascript
  /**
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(words) {
  var row1 = new Set("qwertyuiop");
  var row2 = new Set("asdfghjkl");
  var row3 = new Set("zxcvbnm");

  var result = [];

  for (var i = 0; i < words.length; i++) {
    var word = words[i].toLowerCase();

    var allInOneRow = true;
    var rowSet = row1;

    if (row2.has(word[0])) {
      rowSet = row2;
    } else if (row3.has(word[0])) {
      rowSet = row3;
    }

    for (var j = 1; j < word.length; j++) {
      if (!rowSet.has(word[j])) {
        allInOneRow = false;
        break;
      }
    }

    if (allInOneRow) {
      result.push(words[i]);
    }
  }

  return result;
};

  ```
  