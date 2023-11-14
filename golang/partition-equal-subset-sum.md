
  # partition-equal-subset-sum

  ```golang
  func canPartition(nums []int) bool {
    totalSum := 0
    for _, num := range nums {
        totalSum += num
    }
    
    if totalSum%2 != 0 {
        return false
    }
    
    targetSum := totalSum / 2
    dp := make([]bool, targetSum+1)
    dp[0] = true
    
    for _, num := range nums {
        for j := targetSum; j >= num; j-- {
            dp[j] = dp[j] || dp[j-num]
        }
    }
    
    return dp[targetSum]
}
  ```
  