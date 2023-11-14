
  # string-to-integer-atoi

  ```golang
  func myAtoi(s string) int {
    // Step 1: Ignore leading whitespace
    i := 0
    for i < len(s) && s[i] == ' ' {
        i++
    }
    
    // Step 2: Check if the number is negative or positive
    sign := 1
    if i < len(s) && (s[i] == '-' || s[i] == '+') {
        if s[i] == '-' {
            sign = -1
        }
        i++
    }
    
    // Step 3: Read in the digits
    num := 0
    for i < len(s) && isDigit(s[i]) {
        digit := int(s[i] - '0')
        // Check for overflow
        if num > (math.MaxInt32-digit)/10 {
            if sign == 1 {
                return math.MaxInt32
            } else {
                return math.MinInt32
            }
        }
        num = num*10 + digit
        i++
    }
    
    // Step 4: Apply the sign
    return num * sign
}

func isDigit(c byte) bool {
    return c >= '0' && c <= '9'
}
  ```
  