
  # largest-perimeter-triangle

  ```golang
  func largestPerimeter(nums []int) int {
    sort.Ints(nums)
    n := len(nums)
    maxPerimeter := 0

    for i := n - 1; i >= 2; i-- {
        if nums[i-2]+nums[i-1] > nums[i] {
            // The largest three sides can form a triangle
            maxPerimeter = nums[i-2] + nums[i-1] + nums[i]
            break
        }
    }

    return maxPerimeter
}
  ```
  