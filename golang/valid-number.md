
  # valid-number

  ```golang
  func isNumber(s string) bool {
    // Define a regular expression pattern for a valid number
    pattern := `^[\+\-]?(\d+(\.\d*)?|\.\d+)([eE][\+\-]?\d+)?$`

    // Compile the regular expression
    re := regexp.MustCompile(pattern)

    // Use the MatchString function to check if the string matches the pattern
    return re.MatchString(s)
}

  ```
  