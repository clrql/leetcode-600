
  # count-and-say

  ```javascript
  /**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
    if (n === 1) {
        return "1";
    }
    
    const previous = countAndSay(n - 1);
    let result = "";
    
    let count = 1;
    for (let i = 0; i < previous.length; i++) {
        if (previous[i] === previous[i + 1]) {
            count++;
        } else {
            result += count + previous[i];
            count = 1;
        }
    }
    
    return result;
};
  ```
  