
  # plus-one

  ```c
  /**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* plusOne(int* digits, int digitsSize, int* returnSize) {
    // Add one to the least significant digit
    digits[digitsSize - 1] += 1;

    // Initialize carry
    int carry = 0;

    // Iterate from right to left
    for (int i = digitsSize - 1; i >= 0; i--) {
        digits[i] += carry;

        // Update carry for the next iteration
        carry = digits[i] / 10;
        digits[i] %= 10;
    }

    // If there's still a carry, we need to add an additional digit
    if (carry > 0) {
        (*returnSize) = digitsSize + 1;
        int* result = (int*)malloc((*returnSize) * sizeof(int));
        result[0] = carry;

        // Copy the original digits to the result array
        for (int i = 0; i < digitsSize; i++) {
            result[i + 1] = digits[i];
        }

        return result;
    } else {
        (*returnSize) = digitsSize;
        return digits;
    }
}
  ```
  