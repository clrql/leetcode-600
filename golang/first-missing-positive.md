
  # first-missing-positive

  ```golang
  func firstMissingPositive(nums []int) int {
    // Step 1: Move all positive integers to their respective indices
    n := len(nums)
    for i := 0; i < n; i++ {
        for nums[i] > 0 && nums[i] <= n && nums[nums[i]-1] != nums[i] {
            nums[nums[i]-1], nums[i] = nums[i], nums[nums[i]-1]
        }
    }

    // Step 2: Find the first missing positive integer
    for i := 0; i < n; i++ {
        if nums[i] != i+1 {
            return i + 1
        }
    }

    return n + 1
}



  ```
  