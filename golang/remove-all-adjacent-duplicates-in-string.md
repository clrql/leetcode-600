
  # remove-all-adjacent-duplicates-in-string

  ```golang
  func removeDuplicates(s string) string {
    stack := []rune{} // Use a stack of runes to handle non-ASCII characters

    for _, char := range s {
        if len(stack) > 0 && stack[len(stack)-1] == char {
            // Pop the top character if it's equal to the current character
            stack = stack[:len(stack)-1]
        } else {
            // Push the current character onto the stack
            stack = append(stack, char)
        }
    }

    return string(stack)
}

  ```
  