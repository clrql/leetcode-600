
  # increasing-triplet-subsequence

  ```typescript
  function increasingTriplet(nums: number[]): boolean {
    let smallest = Infinity;
    let secondSmallest = Infinity;

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] <= smallest) {
        smallest = nums[i];
        } else if (nums[i] <= secondSmallest) {
        secondSmallest = nums[i];
        } else {
        // Found a third element greater than both smallest and secondSmallest
        return true;
        }
    }

    return false;
};
  ```
  