
  # goat-latin

  ```golang
  func toGoatLatin(sentence string) string {
    words := strings.Fields(sentence) // Split the sentence into words
    vowels := "aeiouAEIOU" // Define the set of vowels
    result := make([]string, 0)

    for i, word := range words {
        if strings.Contains(vowels, string(word[0])) {
            // If the word starts with a vowel, append "ma" and "a" based on the index
            result = append(result, word+"ma"+strings.Repeat("a", i+1))
        } else {
            // If the word starts with a consonant, move the first letter to the end and append "ma" and "a" based on the index
            result = append(result, word[1:]+string(word[0])+"ma"+strings.Repeat("a", i+1))
        }
    }

    return strings.Join(result, " ") // Join the modified words with spaces
}

  ```
  