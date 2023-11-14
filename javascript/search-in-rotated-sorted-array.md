
  # search-in-rotated-sorted-array

  ```javascript
  /**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (nums[mid] === target) {
      return mid;
    }

    if (nums[left] <= nums[mid]) {
      // Left side is sorted in ascending order
      if (nums[left] <= target && target < nums[mid]) {
        // Target is within the sorted left side
        right = mid - 1;
      } else {
        // Target is on the right side
        left = mid + 1;
      }
    } else {
      // Right side is sorted in ascending order
      if (nums[mid] < target && target <= nums[right]) {
        // Target is within the sorted right side
        left = mid + 1;
      } else {
        // Target is on the left side
        right = mid - 1;
      }
    }
  }

  // Target element not found
  return -1;
};
  ```
  