
  # find-common-characters

  ```golang
  func commonChars(words []string) []string {
    if len(words) == 0 {
        return nil
    }

    // Initialize a hashmap to store character frequencies in the first word
    charCount := make(map[rune]int)
    for _, char := range words[0] {
        charCount[char]++
    }

    // Iterate through the remaining words to update character frequencies
    for i := 1; i < len(words); i++ {
        wordCount := make(map[rune]int)
        for _, char := range words[i] {
            wordCount[char]++
        }

        // Update the character frequencies in charCount to maintain minimum counts
        for char, count := range charCount {
            if wordCount[char] < count {
                charCount[char] = wordCount[char]
            }
        }
    }

    // Create a result slice with the common characters
    var result []string
    for char, count := range charCount {
        for i := 0; i < count; i++ {
            result = append(result, string(char))
        }
    }

    return result
}

  ```
  