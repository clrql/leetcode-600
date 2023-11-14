
  # generate-a-string-with-characters-that-have-odd-counts

  ```javascript
  /**
 * @param {number} n
 * @return {string}
 */
var generateTheString = function(n) {
    let s = ""
    if (!(n % 2)) {
        s += "a"
        n--;
    }
    s += "b".repeat(n)
    return s;
};

// 4
/*

aaab

*/
  ```
  