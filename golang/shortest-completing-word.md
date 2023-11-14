
  # shortest-completing-word

  ```golang
  func shortestCompletingWord(licensePlate string, words []string) string {
	licensePlate = normalizeLicensePlate(licensePlate)
	letterFreq := getLetterFrequency(licensePlate)

	shortestWord := ""
	for _, word := range words {
		if isCompletingWord(word, letterFreq) {
			if shortestWord == "" || len(word) < len(shortestWord) {
				shortestWord = word
			}
		}
	}

	return shortestWord
}

func normalizeLicensePlate(licensePlate string) string {
	licensePlate = strings.ToLower(licensePlate)
	normalized := ""
	for _, ch := range licensePlate {
		if ch >= 'a' && ch <= 'z' {
			normalized += string(ch)
		}
	}
	return normalized
}

func getLetterFrequency(str string) map[rune]int {
	freq := make(map[rune]int)
	for _, ch := range str {
		freq[ch]++
	}
	return freq
}

func isCompletingWord(word string, letterFreq map[rune]int) bool {
	wordFreq := getLetterFrequency(word)

	for ch, count := range letterFreq {
		if wordFreq[ch] < count {
			return false
		}
	}

	return true
}

  ```
  