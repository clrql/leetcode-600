
  # maximum-average-subarray-i

  ```typescript
  function findMaxAverage(nums: number[], k: number): number {
  let sum = 0; // Variable to store the sum of the current subarray
  let maxSum = 0; // Variable to store the maximum sum
  let startIndex = 0; // Start index of the current subarray

  // Calculate the sum of the first k elements
  for (let i = 0; i < k; i++) {
    sum += nums[i];
  }

  maxSum = sum; // Initialize the maximum sum

  // Iterate through the array to find the maximum sum
  for (let i = k; i < nums.length; i++) {
    sum += nums[i] - nums[startIndex]; // Update the sum by adding the current element and subtracting the element at the start index
    maxSum = Math.max(maxSum, sum); // Update the maximum sum if the current sum is greater

    startIndex++; // Move the start index of the subarray forward
  }

  return maxSum / k; // Return the maximum average
}

  ```
  