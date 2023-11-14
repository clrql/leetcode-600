
  # kth-largest-element-in-an-array

  ```typescript
  function findKthLargest(nums: number[], k: number): number {
  const n = nums.length;
  const targetIndex = n - k; // Index of the kth largest element in the sorted order
  let left = 0;
  let right = n - 1;

  while (left <= right) {
    const pivotIndex = partition(nums, left, right);

    if (pivotIndex === targetIndex) {
      return nums[pivotIndex];
    } else if (pivotIndex < targetIndex) {
      left = pivotIndex + 1;
    } else {
      right = pivotIndex - 1;
    }
  }

  return -1; // Invalid input
}

function partition(nums: number[], left: number, right: number): number {
  const pivot = nums[right];
  let i = left;

  for (let j = left; j < right; j++) {
    if (nums[j] <= pivot) {
      swap(nums, i, j);
      i++;
    }
  }

  swap(nums, i, right);

  return i;
}

function swap(nums: number[], i: number, j: number): void {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

  ```
  