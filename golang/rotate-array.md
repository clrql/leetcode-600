
  # rotate-array

  ```golang
  func rotate(nums []int, k int)  {
    k %= len(nums)
    start, end := 0, len(nums)-1
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
    start, end = 0, k-1
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
    start, end = k, len(nums)-1
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
}
  ```
  