
  # monotonic-array

  ```golang
  func isMonotonic(nums []int) bool {
    increasing, decreasing := true, true

    for i := 1; i < len(nums); i++ {
        if nums[i-1] > nums[i] {
            increasing = false
        }
        if nums[i-1] < nums[i] {
            decreasing = false
        }
    }

    return increasing || decreasing
}
  ```
  