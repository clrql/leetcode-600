
  # height-checker

  ```golang
  func heightChecker(heights []int) int {
    n := len(heights)
    expected := make([]int, n)

    // Copy the given heights into the expected array
    copy(expected, heights)

    // Sort the expected array in non-decreasing order
    sort.Ints(expected)

    // Count the number of differing elements
    count := 0
    for i := 0; i < n; i++ {
        if heights[i] != expected[i] {
            count++
        }
    }

    return count
}

  ```
  