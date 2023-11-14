
  # remove-outermost-parentheses

  ```golang
  func removeOuterParentheses(s string) string {
    result := ""
    balance := 0

    for _, char := range s {
        if char == '(' {
            if balance > 0 {
                result += string(char)
            }
            balance++
        } else if char == ')' {
            balance--
            if balance > 0 {
                result += string(char)
            }
        }
    }

    return result
}

  ```
  