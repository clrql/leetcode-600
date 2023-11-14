
  # longest-subarray-of-1s-after-deleting-one-element

  ```typescript
  function longestSubarray(nums: number[]): number {
  let maxLength = 0; // Maximum length of subarray
  let left = 0; // Left pointer
  let zerosCount = 0; // Count of zeros

  for (let right = 0; right < nums.length; right++) {
    if (nums[right] === 0) {
      zerosCount++; // Increment the count of zeros

      while (zerosCount > 1) {
        if (nums[left] === 0) {
          zerosCount--; // Decrement the count of zeros
        }
        left++; // Move the left pointer to the right
      }
    }

    maxLength = Math.max(maxLength, right - left);
  }

  return maxLength;
}

  ```
  