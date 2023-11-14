
  # longest-palindrome

  ```golang
  func longestPalindrome(s string) int {
    freq := make(map[rune]int)
    length := 0
    oddCount := 0
    
    // Count frequencies of characters in the string
    for _, ch := range s {
        freq[ch]++
    }
    
    // Calculate the length of the longest palindrome
    for _, count := range freq {
        length += count / 2 * 2
        if count%2 == 1 {
            oddCount = 1
        }
    }
    
    return length + oddCount
}

  ```
  