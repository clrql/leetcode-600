
  # smallest-range-i

  ```golang
  func smallestRangeI(nums []int, k int) int {
    minVal := min(nums...)
    maxVal := max(nums...)
    
    // Calculate the minimum possible score by adjusting the min and max values
    minScore := maxVal - k - (minVal + k)
    
    // Ensure the score is non-negative
    if minScore < 0 {
        return 0
    }
    
    return minScore
}

func min(nums ...int) int {
    minVal := nums[0]
    for _, num := range nums {
        if num < minVal {
            minVal = num
        }
    }
    return minVal
}

func max(nums ...int) int {
    maxVal := nums[0]
    for _, num := range nums {
        if num > maxVal {
            maxVal = num
        }
    }
    return maxVal
}

  ```
  