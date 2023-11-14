
  # excel-sheet-column-number

  ```golang
  func titleToNumber(columnTitle string) int {
	result := 0

	for _, ch := range columnTitle {
		digit := int(ch - 'A' + 1)
		result = result*26 + digit
	}

	return result
}

  ```
  