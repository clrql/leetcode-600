
  # search-suggestions-system

  ```golang
  func suggestedProducts(products []string, searchWord string) [][]string {
	// Sort the products lexicographically
	sort.Strings(products)
	
	result := make([][]string, len(searchWord))
	prefix := ""

	for i, char := range searchWord {
		prefix += string(char)

		// Binary search for the index of the first product with a prefix >= prefix
		index := sort.SearchStrings(products, prefix)

		// Collect up to three suggested products with the common prefix
		for j := index; j < len(products) && j < index+3; j++ {
			if !startsWith(products[j], prefix) {
				break
			}
			result[i] = append(result[i], products[j])
		}
	}

	return result
}

// Helper function to check if a string starts with a given prefix
func startsWith(s, prefix string) bool {
	if len(s) < len(prefix) {
		return false
	}
	for i := 0; i < len(prefix); i++ {
		if s[i] != prefix[i] {
			return false
		}
	}
	return true
}
  ```
  