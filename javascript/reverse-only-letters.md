
  # reverse-only-letters

  ```javascript
  /**
 * @param {string} s
 * @return {string}
 */
var reverseOnlyLetters = function(s) {
    s = s.split("");

    let left = 0;
    let right = s.length - 1;

    while (left < right) {
        while (left < right && !isLetter(s[left])) left++;
        while (left < right &&!isLetter(s[right])) right--;
        [s[left], s[right]] = [s[right], s[left]];
        left++;
        right--;
    }

    return s.join("");
};

var isLetter = function(char) {
    return /[a-zA-Z]/.test(char);
}
  ```
  