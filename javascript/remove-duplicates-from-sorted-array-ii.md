
  # remove-duplicates-from-sorted-array-ii

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let count = 1; // Count for the current element
  let j = 1; // Position to overwrite duplicates

  for (let i = 1; i < nums.length; i++) {
    // If the current element is the same as the previous one
    if (nums[i] === nums[i - 1]) {
      count++; // Increment the count

      // If the count is less than or equal to 2, keep the element
      if (count <= 2) {
        nums[j] = nums[i]; // Overwrite duplicates
        j++; // Move to the next position to overwrite
      }
    } else {
      // Reset the count for a new element
      count = 1;
      nums[j] = nums[i]; // Overwrite non-duplicates
      j++; // Move to the next position to overwrite
    }
  }

  return j; // Return the new length of the array
}

  ```
  