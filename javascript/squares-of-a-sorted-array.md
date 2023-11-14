
  # squares-of-a-sorted-array

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortedSquares = function(nums) {
    for (let i = 0; i < nums.length; i++) {
        nums[i] = nums[i] ** 2
    }
    return nums.sort((a, b) => a-b)
};
  ```
  