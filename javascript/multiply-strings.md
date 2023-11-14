
  # multiply-strings

  ```javascript
  /**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
var multiply = function(num1, num2) {
    const m = num1.length, n = num2.length;
    const res = Array(m + n).fill(0);
    for (let i = n - 1; i >= 0; i--) {
        let carry = 0;
        for (let j = m - 1; j >= 0; j--) {
            let prod = carry + parseInt(num2.charAt(i)) * parseInt(num1.charAt(j));
            carry = Math.floor(prod / 10);
            res[i + j + 1] += prod % 10;
            res[i + j] += Math.floor(res[i + j + 1] / 10);
            res[i + j + 1] %= 10;
        }
        res[i] += carry;
    }
    let i = 0;
    while (i < m + n && res[i] === 0) {
        i++;
    }
    return i === m + n ? "0" : res.slice(i).join("");
};

  ```
  