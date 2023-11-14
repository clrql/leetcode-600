
  # sort-integers-by-the-number-of-1-bits

  ```javascript
  /**
 * @param {number[]} arr
 * @return {number[]}
 */
var sortByBits = function(arr) {
    return arr.sort((a,b) => a-b).sort((a, b) => a.toString(2).replaceAll("0", "").length - b.toString(2).replaceAll("0", "").length)
};
  ```
  