
  # shortest-palindrome

  ```golang
  func shortestPalindrome(s string) string {
    n := len(s)
    
    // Helper function to check if a string is a palindrome.
    isPalindrome := func(str string) bool {
        i, j := 0, len(str)-1
        for i < j {
            if str[i] != str[j] {
                return false
            }
            i++
            j--
        }
        return true
    }
    
    // Find the longest palindrome prefix.
    i := n - 1
    for i >= 0 && !isPalindrome(s[:i+1]) {
        i--
    }
    
    // Reverse the suffix and concatenate it to the original string.
    suffix := ""
    for j := n - 1; j > i; j-- {
        suffix += string(s[j])
    }
    
    return suffix + s
}

  ```
  