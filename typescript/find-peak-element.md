
  # find-peak-element

  ```typescript
  function findPeakElement(nums: number[]): number {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] > nums[mid + 1]) {
      // The peak is in the left half
      right = mid;
    } else {
      // The peak is in the right half
      left = mid + 1;
    }
  }

  return left;
}
  ```
  