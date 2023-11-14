
  # palindrome-partitioning

  ```golang
  func partition(s string) [][]string {
    var result [][]string
    var current []string
    backtrack(&result, &current, s, 0)
    return result
}

func backtrack(
    result *[][]string, 
    current *[]string, 
    s string, 
    start int) {

    if start >= len(s) {
        temp := make([]string, len(*current))
        copy(temp, *current)
        *result = append(*result, temp)
    }

    for end := start; end < len(s); end++ {
        if isPalindrome(s, start, end) {
            *current = append(*current, s[start:end+1])
            backtrack(result, current, s, end+1)
            *current = (*current)[:len(*current)-1]
        }
    }

}

func isPalindrome(s string, start int, end int) bool {
    for start < end {
        if s[start] != s[end] {
            return false
        }
        start++
        end--
    }
    return true
}


  ```
  