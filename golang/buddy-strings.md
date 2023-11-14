
  # buddy-strings

  ```golang
  func buddyStrings(s string, goal string) bool {
    if len(s) != len(goal) {
        return false
    }
    
    // Case where s and goal are already equal
    if s == goal {
        // Check if there are duplicate characters in s
        charCount := make(map[byte]int)
        for _, char := range s {
            charCount[byte(char)]++
            if charCount[byte(char)] >= 2 {
                return true
            }
        }
        return false
    }
    
    // Find the indices where s and goal differ
    diffIndices := make([]int, 0)
    for i := 0; i < len(s); i++ {
        if s[i] != goal[i] {
            diffIndices = append(diffIndices, i)
        }
    }
    
    // Check if there are exactly two differing indices
    if len(diffIndices) == 2 && s[diffIndices[0]] == goal[diffIndices[1]] && s[diffIndices[1]] == goal[diffIndices[0]] {
        return true
    }
    
    return false
}

  ```
  