
  # number-of-segments-in-a-string

  ```golang
  func countSegments(s string) int {
    count := 0
    inSegment := false

    for _, char := range s {
        if char != ' ' {
            if !inSegment {
                count++
            }
            inSegment = true
        } else {
            inSegment = false
        }
    }

    return count
}
  ```
  