
  # set-mismatch

  ```golang
  func findErrorNums(nums []int) []int {
    n := len(nums)
    numSet := make(map[int]bool)

    duplicate := -1
    for _, num := range nums {
        if numSet[num] {
            duplicate = num
        }
        numSet[num] = true
    }

    missing := -1
    for i := 1; i <= n; i++ {
        if !numSet[i] {
            missing = i
            break
        }
    }

    return []int{duplicate, missing}
}

  ```
  