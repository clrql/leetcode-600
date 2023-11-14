
  # unique-morse-code-words

  ```golang
  func uniqueMorseRepresentations(words []string) int {
    morseCodes := []string{
        ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..", ".---", "-.-", ".-..", "--",
        "-.", "---", ".--.", "--.-", ".-.", "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--..",
    }

    uniqueTransformations := make(map[string]bool)

    for _, word := range words {
        transformation := ""
        for _, letter := range word {
            transformation += morseCodes[letter-'a']
        }
        uniqueTransformations[transformation] = true
    }

    return len(uniqueTransformations)
}

  ```
  