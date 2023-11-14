
  # validate-stack-sequences

  ```golang
  func validateStackSequences(pushed []int, popped []int) bool {
    stack := make([]int, 0)
    i := 0
    for _, x := range pushed {
        stack = append(stack, x)
        for len(stack) > 0 && stack[len(stack)-1] == popped[i] {
            stack = stack[:len(stack)-1]
            i++
        }
    }
    return i == len(popped)
}
  ```
  