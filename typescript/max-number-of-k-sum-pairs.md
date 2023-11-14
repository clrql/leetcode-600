
  # max-number-of-k-sum-pairs

  ```typescript
  function maxOperations(nums: number[], k: number): number {
  const numCount = new Map<number, number>(); // Map to store the count of each number

  let operations = 0; // Count of operations

  for (const num of nums) {
    const complement = k - num; // Find the complement number to form the sum k

    if (numCount.has(complement) && numCount.get(complement) > 0) {
      // Found a pair that sums up to k
      operations++;
      numCount.set(complement, numCount.get(complement)! - 1); // Decrease the count of the complement number
    } else {
      // Update the count of the current number
      numCount.set(num, (numCount.get(num) || 0) + 1);
    }
  }

  return operations;
}

  ```
  