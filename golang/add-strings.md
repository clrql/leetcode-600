
  # add-strings

  ```golang
  
func addStrings(num1 string, num2 string) string {
	i := len(num1) - 1
	j := len(num2) - 1
	carry := 0
	var result strings.Builder

	for i >= 0 || j >= 0 || carry > 0 {
		sum := carry

		if i >= 0 {
			sum += int(num1[i] - '0')
			i--
		}

		if j >= 0 {
			sum += int(num2[j] - '0')
			j--
		}

		result.WriteString(strconv.Itoa(sum % 10))
		carry = sum / 10
	}

	// Reverse the result
	bytes := []byte(result.String())
	for left, right := 0, len(bytes)-1; left < right; left, right = left+1, right-1 {
		bytes[left], bytes[right] = bytes[right], bytes[left]
	}

	return string(bytes)
}
  ```
  