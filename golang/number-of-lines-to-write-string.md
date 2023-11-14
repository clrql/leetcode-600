
  # number-of-lines-to-write-string

  ```golang
  func numberOfLines(widths []int, s string) []int {
    lineCount := 1
    lineWidth := 0
    
    for _, char := range s {
        charWidth := widths[char-'a']
        if lineWidth+charWidth > 100 {
            lineCount++
            lineWidth = charWidth
        } else {
            lineWidth += charWidth
        }
    }
    
    return []int{lineCount, lineWidth}
}

  ```
  