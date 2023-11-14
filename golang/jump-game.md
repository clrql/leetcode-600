
  # jump-game

  ```golang
  func canJump(nums []int) bool {
    maxReach := 0 // The maximum index that can be reached so far

    for i := 0; i < len(nums); i++ {
        // If the current index is not reachable, return false
        if i > maxReach {
            return false
        }

        // Update the maximum reach if the current index + jump length is greater
        if i+nums[i] > maxReach {
            maxReach = i + nums[i]
        }

        // If the maximum reach is already the last index, return true
        if maxReach >= len(nums)-1 {
            return true
        }
    }

    return false // The last index is not reachable
}
  ```
  