
  # move-zeroes

  ```golang
  func moveZeroes(nums []int)  {
    // Initialize a pointer to the first zero
    zeroPtr := 0

    // Iterate through the array
    for i := 0; i < len(nums); i++ {
        // If the current element is non-zero
        if nums[i] != 0 {
            // Swap the current element with the element at the first zero pointer
            nums[i], nums[zeroPtr] = nums[zeroPtr], nums[i]
            // Move the zero pointer one position to the right
            zeroPtr++
        }
    }
}
  ```
  