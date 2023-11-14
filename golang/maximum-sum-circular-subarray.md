
  # maximum-sum-circular-subarray

  ```golang
  func maxSubarraySumCircular(nums []int) int {
    // Case 1: Maximum sum subarray is not circular
    maxSum := kadane(nums)
    
    // Case 2: Maximum sum subarray is circular
    // In this case, we subtract the minimum sum subarray from the total sum of the array
    totalSum := 0
    for i := 0; i < len(nums); i++ {
        totalSum += nums[i]
        nums[i] = -nums[i]
    }
    circularSum := totalSum + kadane(nums)
    
    // Return the maximum of the two cases
    if circularSum > maxSum && circularSum != 0 {
        return circularSum
    }
    return maxSum
}

// Kadane's algorithm to find the maximum sum subarray
func kadane(nums []int) int {
    maxSum := nums[0]
    currentSum := nums[0]
    
    for i := 1; i < len(nums); i++ {
        currentSum = max(nums[i], currentSum+nums[i])
        maxSum = max(maxSum, currentSum)
    }
    
    return maxSum
}

// Helper function to find the maximum of two integers
func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
  ```
  