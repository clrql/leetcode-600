
  # build-an-array-with-stack-operations

  ```golang
  func buildArray(target []int, n int) []string {
    result := []string{}
    currentIndex := 0

    for i := 1; i <= n && currentIndex < len(target); i++ {
        result = append(result, "Push")
        if i == target[currentIndex] {
            currentIndex++
        } else {
            result = append(result, "Pop")
        }
    }

    return result
}
  ```
  