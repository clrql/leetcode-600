
  # 132-pattern

  ```golang
  func find132pattern(nums []int) bool {
    n := len(nums)
    if n < 3 {
        return false
    }
    
    minStack := make([]int, n)
    minStack[0] = nums[0]
    
    for i := 1; i < n; i++ {
        minStack[i] = min(minStack[i-1], nums[i])
    }
    
    stack := []int{}
    
    for j := n - 1; j >= 0; j-- {
        if nums[j] > minStack[j] {
            for len(stack) > 0 && stack[len(stack)-1] <= minStack[j] {
                stack = stack[:len(stack)-1]
            }
            if len(stack) > 0 && stack[len(stack)-1] < nums[j] {
                return true
            }
            stack = append(stack, nums[j])
        }
    }
    
    return false
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

  ```
  