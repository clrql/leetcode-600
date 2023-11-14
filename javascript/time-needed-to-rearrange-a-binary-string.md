
  # time-needed-to-rearrange-a-binary-string

  ```javascript
  /**
 * @param {string} s
 * @return {number}
 */
var secondsToRemoveOccurrences = function(s) {
    let seconds = 0;

    while (s.includes("01")) {
        s = s.replace(/01/g, "10");
        seconds++;
    }

    return seconds;
};
  ```
  