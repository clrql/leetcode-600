
  # backspace-string-compare

  ```javascript
  /**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var backspaceCompare = function(s, t) {
    const getNextValidCharIndex = (str, index) => {
        let backspaceCount = 0;
        while (index >= 0) {
            if (str[index] === '#') {
                backspaceCount++;
            } else if (backspaceCount > 0) {
                backspaceCount--;
            } else {
                break;
            }
            index--;
        }
        return index;
    }

    let sIndex = s.length - 1;
    let tIndex = t.length - 1;

    while (sIndex >= 0 || tIndex >= 0) {
        sIndex = getNextValidCharIndex(s, sIndex);
        tIndex = getNextValidCharIndex(t, tIndex);

        if (sIndex < 0 && tIndex < 0) {
            return true;
        }
        if (sIndex < 0 || tIndex < 0 || s[sIndex] !== t[tIndex]) {
            return false;
        }

        sIndex--;
        tIndex--;
    }

    return true;
};
  ```
  