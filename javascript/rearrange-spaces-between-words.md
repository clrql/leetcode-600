
  # rearrange-spaces-between-words

  ```javascript
  /**
 * @param {string} text
 * @return {string}
 */
var reorderSpaces = function(text) {
    let spaces = text.replaceAll(/[^ ]/g, "").length; // 2nd way: Array.from(text.matchAll(/[ ]/g))
    let words = text.trim().split(/ +/);

    let remainder = spaces % (words.length - 1);
    let separator = " ".repeat((spaces-remainder)/(words.length - 1));

    if (words.length == 1) return words.join("") + " ".repeat(spaces);

    return words.join(separator) + " ".repeat(remainder);
};
  ```
  