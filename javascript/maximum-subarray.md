
  # maximum-subarray

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let max = nums[0];
    let curr = 0;
    for (let num of nums) {
        curr = Math.max(num, curr + num);
        if (curr > max) {
            max = curr;
        }
    }
    return max;
};
  ```
  