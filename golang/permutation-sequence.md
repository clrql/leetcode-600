
  # permutation-sequence

  ```golang
  func getPermutation(n int, k int) string {
    fact := make([]int, n)
    numbers := make([]int, n)
    
    fact[0] = 1
    for i := 1; i < n; i++ {
        fact[i] = fact[i-1] * i
    }
    
    for i := 1; i <= n; i++ {
        numbers[i-1] = i
    }
    
    k-- // Convert to 0-based index
    
    var result strings.Builder
    for i := n; i >= 1; i-- {
        index := k / fact[i-1]
        k %= fact[i-1]
        
        result.WriteString(strconv.Itoa(numbers[index]))
        numbers = append(numbers[:index], numbers[index+1:]...)
    }
    
    return result.String()
}

  ```
  