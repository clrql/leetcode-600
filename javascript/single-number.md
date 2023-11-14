
  # single-number

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = (nums) => nums.reduce((acc, e) => acc ^ e);
  ```
  