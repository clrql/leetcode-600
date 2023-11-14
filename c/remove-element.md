
  # remove-element

  ```c
  int removeElement(int* nums, int numsSize, int val) {
    int nonValCount = 0; // Count of elements not equal to val

    for (int i = 0; i < numsSize; i++) {
        if (nums[i] != val) {
            nums[nonValCount] = nums[i];
            nonValCount++;
        }
    }

    return nonValCount;
}
  ```
  