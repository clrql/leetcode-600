
  # longest-substring-without-repeating-characters

  ```golang
  func lengthOfLongestSubstring(s string) int {
    charSet := make(map[byte]bool)
    left, right := 0, 0
    maxLength := 0

    for right < len(s) {
        if _, found := charSet[s[right]]; !found {
            charSet[s[right]] = true
            right++
            maxLength = max(maxLength, len(charSet))
        } else {
            delete(charSet, s[left])
            left++
        }
    }

    return maxLength
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  