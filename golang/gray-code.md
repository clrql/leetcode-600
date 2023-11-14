
  # gray-code

  ```golang
  func grayCode(n int) []int {
    result := make([]int, 0, 1<<uint(n))

    for i := 0; i < 1<<uint(n); i++ {
        result = append(result, i^(i>>1))
    }

    return result
}

  ```
  