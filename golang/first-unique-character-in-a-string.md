
  # first-unique-character-in-a-string

  ```golang
  func firstUniqChar(s string) int {
    freq := make(map[rune]int)
    
    // Count frequencies of characters in the string
    for _, ch := range s {
        freq[ch]++
    }
    
    // Find the first character with frequency 1
    for i, ch := range s {
        if freq[ch] == 1 {
            return i
        }
    }
    
    return -1
}

  ```
  