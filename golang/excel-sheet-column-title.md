
  # excel-sheet-column-title

  ```golang
  func convertToTitle(columnNumber int) string {
	var result string

	for columnNumber > 0 {
		columnNumber--  // Adjust columnNumber to be 0-based
		result = string('A'+columnNumber%26) + result
		columnNumber /= 26
	}

	return result
}
  ```
  