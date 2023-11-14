
  # binary-number-with-alternating-bits

  ```golang
  func hasAlternatingBits(n int) bool {
    binary := fmt.Sprintf("%b", n)

    for i := 1; i < len(binary); i++ {
        if binary[i] == binary[i-1] {
            return false
        }
    }

    return true
}

  ```
  