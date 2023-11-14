
  # happy-number

  ```javascript
  /**
 * @param {number} n
 * @return {boolean}
 */
var isHappy = function(n) {
    if (n == 1) return true;
    let seen = [n];
    while (true) {
        n = n
            .toString()
            .split("")
            .map(e => parseInt(e))
            .map(e => e**2)
            .reduce((acc, cur) => acc + cur, 0)
        if (seen.includes(n)) {
            return false;
        }
        seen.push(n);
        if (n == 1) return true;
    }
};
  ```
  