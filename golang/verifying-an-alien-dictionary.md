
  # verifying-an-alien-dictionary

  ```golang
  func isAlienSorted(words []string, order string) bool {
    alienOrder := make(map[byte]int)
    for i, char := range order {
        alienOrder[byte(char)] = i
    }

    for i := 1; i < len(words); i++ {
        if !isLexicographicallySorted(words[i-1], words[i], alienOrder) {
            return false
        }
    }

    return true
}

func isLexicographicallySorted(word1, word2 string, alienOrder map[byte]int) bool {
    i, j := 0, 0
    for i < len(word1) && j < len(word2) {
        if alienOrder[word1[i]] < alienOrder[word2[j]] {
            return true
        } else if alienOrder[word1[i]] > alienOrder[word2[j]] {
            return false
        }
        i++
        j++
    }

    return i == len(word1) || j < len(word2)
}

  ```
  