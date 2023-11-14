
  # shortest-distance-to-a-character

  ```golang
  func shortestToChar(s string, c byte) []int {
    n := len(s)
    
    // Initialize an array to store the distances
    distances := make([]int, n)
    
    // Initialize variables to keep track of the leftmost and rightmost occurrences of 'c'
    leftmost := -n
    rightmost := 2 * n
    
    // Iterate through the string from left to right
    for i := 0; i < n; i++ {
        if s[i] == c {
            leftmost = i
        }
        distances[i] = i - leftmost
    }
    
    // Iterate through the string from right to left
    for i := n - 1; i >= 0; i-- {
        if s[i] == c {
            rightmost = i
        }
        distances[i] = min(distances[i], rightmost - i)
    }
    
    return distances
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

  ```
  