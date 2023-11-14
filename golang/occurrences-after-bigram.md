
  # occurrences-after-bigram

  ```golang
  func findOcurrences(text string, first string, second string) []string {
	words := strings.Fields(text)
	result := make([]string, 0)

	for i := 0; i < len(words)-2; i++ {
		if words[i] == first && words[i+1] == second {
			result = append(result, words[i+2])
		}
	}

	return result
}
  ```
  