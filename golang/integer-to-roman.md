
  # integer-to-roman

  ```golang
  func intToRoman(num int) string {
    symbols := []string{"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"}
    values := []int{1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1}

    roman := ""
    for i := 0; i < len(symbols); i++ {
        for num >= values[i] {
            roman += symbols[i]
            num -= values[i]
        }
    }

    return roman
}
  ```
  