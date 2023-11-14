
  # sort-colors

  ```javascript
  /**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let low = 0;          // pointer for 0
    let mid = 0;          // pointer for 1
    let high = nums.length - 1;  // pointer for 2

    while (mid <= high) {
        if (nums[mid] === 0) {
        // Swap the current element with the element at the low pointer
        [nums[mid], nums[low]] = [nums[low], nums[mid]];
        low++;
        mid++;
        } else if (nums[mid] === 1) {
        // Move to the next element
        mid++;
        } else if (nums[mid] === 2) {
        // Swap the current element with the element at the high pointer
        [nums[mid], nums[high]] = [nums[high], nums[mid]];
        high--;
        }
    }
};
  ```
  