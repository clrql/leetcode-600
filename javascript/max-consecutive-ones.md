
  # max-consecutive-ones

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var findMaxConsecutiveOnes = function(nums) {
  var maxConsecutive = 0;
  var currentConsecutive = 0;

  for (var i = 0; i < nums.length; i++) {
    if (nums[i] === 1) {
      currentConsecutive++;
      maxConsecutive = Math.max(maxConsecutive, currentConsecutive);
    } else {
      currentConsecutive = 0;
    }
  }

  return maxConsecutive;
};

  ```
  