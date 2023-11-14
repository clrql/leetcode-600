
  # ransom-note

  ```golang
  func canConstruct(ransomNote string, magazine string) bool {
    // Create a frequency map for characters in the magazine
    magazineMap := make(map[rune]int)
    for _, ch := range magazine {
        magazineMap[ch]++
    }
    
    // Check if the ransom note can be constructed
    for _, ch := range ransomNote {
        count, exists := magazineMap[ch]
        if !exists || count == 0 {
            return false
        }
        magazineMap[ch]--
    }
    
    return true
}

  ```
  