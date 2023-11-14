
  # unique-length-3-palindromic-subsequences

  ```golang
  func countPalindromicSubsequence(s string) int {
    count := 0
    for i := 'a'; i <= 'z'; i++ {
        first, last := -1, -1
        for j := 0; j < len(s); j++ {
            if rune(s[j]) == i {
                if first == -1 {
                    first = j
                }
                last = j
            }
        }
        if first != -1 && last != -1 && last-first > 1 {
            count += len(uniqueSubsequences(s[first+1:last]))
        }
    }
    return count
}

func uniqueSubsequences(s string) map[rune]bool {
    result := make(map[rune]bool)
    for _, char := range s {
        result[char] = true
    }
    return result
}

  ```
  