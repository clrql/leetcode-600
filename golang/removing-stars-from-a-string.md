
  # removing-stars-from-a-string

  ```golang
  func removeStars(s string) string {
    // Convert the string to a slice of runes for easier manipulation.
    chars := []rune(s)
    // Use two pointers: i for iterating through the string, and j for keeping track of the valid characters.
    j := 0
    for i := 0; i < len(chars); i++ {
        if chars[i] != '*' {
            chars[j] = chars[i]
            j++
        } else {
            j--
        }
    }
    // Convert the slice of runes back to a string and return it.
    return string(chars[:j])
}

  ```
  