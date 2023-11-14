
  # uncommon-words-from-two-sentences

  ```golang
  func uncommonFromSentences(s1 string, s2 string) []string {
    words1 := strings.Fields(s1)
    words2 := strings.Fields(s2)

    wordCount := make(map[string]int)

    for _, word := range words1 {
        wordCount[word]++
    }

    for _, word := range words2 {
        wordCount[word]++
    }

    uncommonWords := []string{}

    for word, count := range wordCount {
        if count == 1 {
            uncommonWords = append(uncommonWords, word)
        }
    }

    return uncommonWords
}
  ```
  