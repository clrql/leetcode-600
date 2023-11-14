
  # sort-vowels-in-a-string

  ```golang
  func isVowel(c byte) bool {
	vowels := "aeiouAEIOU"
	return strings.ContainsRune(vowels, rune(c))
}

func sortVowels(s string) string {
	vowelIndices := make([]int, 0)
	vowels := make([]byte, 0)

	// Find vowel indices and collect vowels
	for i := 0; i < len(s); i++ {
		if isVowel(s[i]) {
			vowelIndices = append(vowelIndices, i)
			vowels = append(vowels, s[i])
		}
	}

	// Sort vowels
	sort.Slice(vowels, func(i, j int) bool {
		return vowels[i] < vowels[j]
	})

	// Reconstruct the final string
	result := make([]byte, len(s))
	copy(result, []byte(s))

	for i := 0; i < len(vowels); i++ {
		result[vowelIndices[i]] = vowels[i]
	}

	return string(result)
}

  ```
  