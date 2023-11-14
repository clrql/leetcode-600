
  # di-string-match

  ```golang
  func diStringMatch(s string) []int {
    n := len(s)
    result := make([]int, n+1)
    low, high := 0, n
    
    for i := 0; i < n; i++ {
        if s[i] == 'I' {
            result[i] = low
            low++
        } else {
            result[i] = high
            high--
        }
    }
    
    result[n] = low  // or high, they will be equal at this point
    return result
}
  ```
  