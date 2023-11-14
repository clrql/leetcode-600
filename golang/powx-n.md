
  # powx-n

  ```golang
  func myPow(x float64, n int) float64 {
    // Any number to the power 0 is equal to 1
    if n == 0 {
        return 1
    }
    // If the power is a negative number we invert the value of x and change make n positive.
    if n < 0 {
        x = 1 / x
        n = -n
    }
    res := 1.0
    for n > 0 {
        if n%2 == 1 {
            res *= x
        }
        x *= x
        n /= 2
    }
    return res
}
  ```
  