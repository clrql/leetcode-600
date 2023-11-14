
  # longest-continuous-increasing-subsequence

  ```golang
  func findLengthOfLCIS(nums []int) int {
    maxLen := 0
    currentLen := 0

    for i := 0; i < len(nums); i++ {
        if i == 0 || nums[i] > nums[i-1] {
            currentLen++
        } else {
            maxLen = max(maxLen, currentLen)
            currentLen = 1
        }
    }

    maxLen = max(maxLen, currentLen)

    return maxLen
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  