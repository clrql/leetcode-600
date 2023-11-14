
  # max-consecutive-ones-iii

  ```typescript
  function longestOnes(nums: number[], k: number): number {
  let maxConsecutiveOnes = 0; // Maximum consecutive ones
  let left = 0; // Left pointer
  let zerosCount = 0; // Count of zeros

  for (let right = 0; right < nums.length; right++) {
    if (nums[right] === 0) {
      zerosCount++; // Increment the count of zeros
    }

    while (zerosCount > k) {
      if (nums[left] === 0) {
        zerosCount--; // Decrement the count of zeros
      }
      left++; // Move the left pointer to the right
    }

    maxConsecutiveOnes = Math.max(maxConsecutiveOnes, right - left + 1);
  }

  return maxConsecutiveOnes;
}

  ```
  