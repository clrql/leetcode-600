
  # self-dividing-numbers

  ```golang
  func selfDividingNumbers(left int, right int) []int {
    var result []int
    for num := left; num <= right; num++ {
        if isSelfDividing(num) {
            result = append(result, num)
        }
    }
    return result
}

func isSelfDividing(num int) bool {
    n := num
    for n > 0 {
        digit := n % 10
        if digit == 0 || num%digit != 0 {
            return false
        }
        n /= 10
    }
    return true
}

  ```
  