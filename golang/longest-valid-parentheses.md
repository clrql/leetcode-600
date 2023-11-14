
  # longest-valid-parentheses

  ```golang
  func longestValidParentheses(s string) int {
    stack := []int{-1} // Initialize the stack with -1
    maxLen := 0

    for i, ch := range s {
        if ch == '(' {
            stack = append(stack, i) // Push the index of '(' to the stack
        } else {
            stack = stack[:len(stack)-1] // Pop the top element from the stack

            if len(stack) == 0 {
                stack = append(stack, i) // Push the current index as a potential starting point
            } else {
                currLen := i - stack[len(stack)-1] // Calculate the current valid substring length

                if currLen > maxLen {
                    maxLen = currLen
                }
            }
        }
    }

    return maxLen
}
  ```
  