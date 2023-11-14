
  # find-the-duplicate-number

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
 //Floyd's Tortoise
var findDuplicate = function(nums) {
  let slow = nums[0];
  let fast = nums[0];

  // Move slow by 1 step and fast by 2 steps until they meet
  do {
    slow = nums[slow];
    fast = nums[nums[fast]];
  } while (slow !== fast);

  // Move slow back to the start and keep fast at the meeting point
  slow = nums[0];
  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[fast];
  }

  return slow; // Return the repeated number
};
  ```
  