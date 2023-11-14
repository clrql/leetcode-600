
  # maximum-product-subarray

  ```typescript
  function maxProduct(nums: number[]): number {
  let maxProduct = nums[0];
  let currMax = nums[0];
  let currMin = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] < 0) {
      // Swap current maximum and minimum
      [currMax, currMin] = [currMin, currMax];
    }

    currMax = Math.max(nums[i], currMax * nums[i]);
    currMin = Math.min(nums[i], currMin * nums[i]);

    maxProduct = Math.max(maxProduct, currMax);
  }

  return maxProduct;
}
  ```
  