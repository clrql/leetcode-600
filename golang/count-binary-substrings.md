
  # count-binary-substrings

  ```golang
  func countBinarySubstrings(s string) int {
    prevCount := 0
    currCount := 1
    count := 0

    for i := 1; i < len(s); i++ {
        if s[i] == s[i-1] {
            currCount++
        } else {
            prevCount = currCount
            currCount = 1
        }

        if prevCount >= currCount {
            count++
        }
    }

    return count
}

  ```
  