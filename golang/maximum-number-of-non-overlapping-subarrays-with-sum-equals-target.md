
  # maximum-number-of-non-overlapping-subarrays-with-sum-equals-target

  ```golang
  func maxNonOverlapping(nums []int, target int) int {
    var total int = 0
    var result int = 0
    var seen = make(map[int]bool)
    for _, val := range nums {
        total += val;
        if total == target || seen[total - target] {
            total = 0;
            result++;
            seen = make(map[int]bool)
        } else {
            seen[total] = true
        }
    }
    return result
}
  ```
  