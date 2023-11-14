
  # student-attendance-record-i

  ```javascript
  /**
 * @param {string} s
 * @return {boolean}
 */
var checkRecord = function(s) {
  var absentCount = 0;
  var lateCount = 0;

  for (var i = 0; i < s.length; i++) {
    if (s[i] === 'A') {
      absentCount++;
      if (absentCount >= 2) {
        return false;
      }
    }

    if (s[i] === 'L') {
      lateCount++;
      if (lateCount >= 3) {
        return false;
      }
    } else {
      lateCount = 0;
    }
  }

  return true;
};

  ```
  