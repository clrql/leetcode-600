
  # remove-duplicates-from-sorted-array

  ```c
  int removeDuplicates(int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0;
    }

    int uniqueCount = 1; // Initialize with 1 for the first element
    int i;

    for (i = 1; i < numsSize; i++) {
        if (nums[i] != nums[i - 1]) {
            nums[uniqueCount] = nums[i];
            uniqueCount++;
        }
    }

    return uniqueCount;
}
  ```
  