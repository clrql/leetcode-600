
  # guess-number-higher-or-lower

  ```javascript
  /** 
 * Forward declaration of guess API.
 * @param {number} num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * var guess = function(num) {}
 */

/**
 * @param {number} n
 * @return {number}
 */
var guessNumber = function(n) {
    let low = 1;
    let high = n;
    while (low <= high) {
        let m = Math.ceil(low + (high - low) / 2);
        let r = guess(m);
        if (r < 0) {
            high = m - 1;
        } else if (r == 0) {
            return m;
        } else {
            low = m + 1;
        }
    }
    return -1;
};
  ```
  