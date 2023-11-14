
  # divide-two-integers

  ```golang
  func divide(dividend int, divisor int) int {

    if divisor == 0 || (dividend == math.MinInt32 && divisor == -1) {
        return math.MaxInt32;
    }

    sign := 1;
    if (dividend < 0 && divisor > 0) || (dividend > 0 && divisor < 0) {
        sign = -1;
    }
    a, b := abs(dividend), abs(divisor)
    quotient := 0
    for a >= b {
        temp, multiple := b, 1
        for a >= (temp << 1) {
            temp <<= 1
            multiple <<= 1
        }
        a -= temp
        quotient += multiple
    }
    return sign*quotient
}

func abs(num int) int {
    if num < 0 {
        return -num
    }
    return num
}
  ```
  