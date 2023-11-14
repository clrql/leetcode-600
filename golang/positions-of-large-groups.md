
  # positions-of-large-groups

  ```golang
  func largeGroupPositions(s string) [][]int {
    result := make([][]int, 0)
    n := len(s)
    
    for i := 0; i < n; {
        char := s[i]
        start := i
        count := 0
        
        // Count consecutive characters
        for i < n && s[i] == char {
            count++
            i++
        }
        
        // Check if the group is large (count >= 3)
        if count >= 3 {
            result = append(result, []int{start, i - 1})
        }
    }
    
    return result
}

  ```
  