
  # word-ladder

  ```golang
  func ladderLength(beginWord string, endWord string, wordList []string) int {
	// Convert wordList to a set for efficient word lookup
	wordSet := make(map[string]bool)
	for _, word := range wordList {
		wordSet[word] = true
	}

	// If endWord is not in the wordList, there is no valid transformation sequence
	if !wordSet[endWord] {
		return 0
	}

	// Perform BFS starting from the beginWord
	queue := []string{beginWord}
	visited := make(map[string]bool)
	visited[beginWord] = true
	level := 1

	for len(queue) > 0 {
		size := len(queue)

		// Process all words at the current level
		for i := 0; i < size; i++ {
			word := queue[0]
			queue = queue[1:]

			// Generate all possible transformations of the word
			for j := 0; j < len(word); j++ {
				for ch := 'a'; ch <= 'z'; ch++ {
					newWord := word[:j] + string(ch) + word[j+1:]

					// If the newWord is in the wordSet and not visited yet, enqueue it
					if wordSet[newWord] && !visited[newWord] {
						if newWord == endWord {
							return level + 1 // Found the endWord
						}
						queue = append(queue, newWord)
						visited[newWord] = true
					}
				}
			}
		}

		level++
	}

	return 0 // No transformation sequence found
}
  ```
  