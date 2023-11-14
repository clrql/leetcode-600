
  # next-permutation

  ```golang
  func nextPermutation(nums []int) {
    // Find the first decreasing element from the right
    i := len(nums) - 2
    for i >= 0 && nums[i] >= nums[i+1] {
        i--
    }

    // If such element exists, find the next greater element to its right
    if i >= 0 {
        j := len(nums) - 1
        for j > i && nums[j] <= nums[i] {
            j--
        }
        // Swap the two elements
        nums[i], nums[j] = nums[j], nums[i]
    }

    // Reverse the subarray to the right of i
    reverse(nums, i+1, len(nums)-1)
}

// Helper function to reverse a subarray in place
func reverse(nums []int, start, end int) {
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
}

  ```
  