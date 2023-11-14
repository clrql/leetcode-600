
  # decode-string

  ```golang
  func decodeString(s string) string {
	stack := make([]string, 0)
	numStack := make([]int, 0)
	currentString := ""

	for i := 0; i < len(s); i++ {
		if s[i] >= '0' && s[i] <= '9' {
			// Parse the number
			num := 0
			for ; i < len(s) && s[i] >= '0' && s[i] <= '9'; i++ {
				num = num*10 + int(s[i]-'0')
			}
			i-- // Move the index back by one to reprocess the current character

			numStack = append(numStack, num)
		} else if s[i] == '[' {
			// Push the currentString to the stack
			stack = append(stack, currentString)

			// Reset the currentString
			currentString = ""
		} else if s[i] == ']' {
			// Retrieve the previous string from the stack
			prevString := stack[len(stack)-1]
			stack = stack[:len(stack)-1]

			// Retrieve the previous number from the number stack
			num := numStack[len(numStack)-1]
			numStack = numStack[:len(numStack)-1]

			// Repeat the current string by the previous number
			currentString = prevString + strings.Repeat(currentString, num)
		} else {
			// Append the current character to the currentString
			currentString += string(s[i])
		}
	}

	return currentString
}
  ```
  