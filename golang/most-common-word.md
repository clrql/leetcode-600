
  # most-common-word

  ```golang
  func mostCommonWord(paragraph string, banned []string) string {
    // Preprocess the paragraph: lowercase and split into words
    paragraph = strings.ToLower(paragraph)
    words := make([]string, 0)
    wordStart := -1

    for i, char := range paragraph {
        if isLetter(char) {
            if wordStart == -1 {
                wordStart = i
            }
        } else {
            if wordStart != -1 {
                words = append(words, paragraph[wordStart:i])
                wordStart = -1
            }
        }
    }

    if wordStart != -1 {
        words = append(words, paragraph[wordStart:])
    }

    // Create a map to store word frequency counts
    wordCount := make(map[string]int)

    // Create a set of banned words for faster lookup
    bannedSet := make(map[string]bool)
    for _, word := range banned {
        bannedSet[word] = true
    }

    // Iterate through words and count frequencies
    mostCommon := ""
    maxCount := 0

    for _, word := range words {
        if !bannedSet[word] {
            wordCount[word]++
            if wordCount[word] > maxCount {
                maxCount = wordCount[word]
                mostCommon = word
            }
        }
    }

    return mostCommon
}

func isLetter(char rune) bool {
    return (char >= 'a' && char <= 'z') || (char >= 'A' && char <= 'Z')
}

  ```
  