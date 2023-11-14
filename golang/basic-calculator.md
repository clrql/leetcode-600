
  # basic-calculator

  ```golang
  func calculate(s string) int {
	stack := make([]int, 0)
	sign := 1 // represents the sign of the current expression
	result := 0
	num := 0

	for i := 0; i < len(s); i++ {
		if isDigit(s[i]) {
			// Calculate the number by iterating over consecutive digits
			num = num*10 + int(s[i]-'0')
		} else if s[i] == '+' {
			// Add the number to the result with the appropriate sign
			result += sign * num
			num = 0 // reset the number
			sign = 1 // reset the sign for the next expression
		} else if s[i] == '-' {
			// Add the number to the result with the appropriate sign
			result += sign * num
			num = 0 // reset the number
			sign = -1 // reset the sign for the next expression
		} else if s[i] == '(' {
			// Push the result and sign onto the stack
			stack = append(stack, result, sign)
			result = 0 // reset the result for the sub-expression
			sign = 1 // reset the sign for the sub-expression
		} else if s[i] == ')' {
			// Evaluate the sub-expression by popping the result and sign from the stack
			result += sign * num
			num = 0 // reset the number

			sign = stack[len(stack)-1] // restore the sign
			stack = stack[:len(stack)-1] // pop the sign from the stack
			prevResult := stack[len(stack)-1] // get the previous result
			stack = stack[:len(stack)-1] // pop the previous result from the stack
			result = prevResult + sign*result // calculate the new result
			sign = 1 // reset the sign for the next expression
		}
	}

	// Add the last number to the result with the appropriate sign
	result += sign * num

	return result
}

func isDigit(ch byte) bool {
	return ch >= '0' && ch <= '9'
}


  ```
  