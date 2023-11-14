
  # unique-email-addresses

  ```golang
  func numUniqueEmails(emails []string) int {
    uniqueEmails := make(map[string]bool)

    for _, email := range emails {
        normalizedEmail := normalizeEmail(email)
        uniqueEmails[normalizedEmail] = true
    }

    return len(uniqueEmails)
}

func normalizeEmail(email string) string {
    parts := strings.Split(email, "@")
    localName := parts[0]
    domainName := parts[1]

    localName = strings.Split(localName, "+")[0] // Remove everything after '+'
    localName = strings.ReplaceAll(localName, ".", "") // Remove all '.' characters

    return localName + "@" + domainName
}

  ```
  