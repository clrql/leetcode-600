
  # add-to-array-form-of-integer

  ```golang
  func addToArrayForm(num []int, k int) []int {
    n := len(num)
    carry := 0
    result := make([]int, n)

    for i := n - 1; i >= 0; i-- {
        digitSum := num[i] + k%10 + carry
        carry = digitSum / 10
        result[i] = digitSum % 10
        k /= 10
    }

    // Process any remaining carry from k
    for k > 0 {
        digitSum := k%10 + carry
        carry = digitSum / 10
        result = append([]int{digitSum % 10}, result...)
        k /= 10
    }

    // Process any remaining carry
    for carry > 0 {
        result = append([]int{carry % 10}, result...)
        carry /= 10
    }

    return result
}

  ```
  