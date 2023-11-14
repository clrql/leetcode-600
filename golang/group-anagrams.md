
  # group-anagrams

  ```golang
  func groupAnagrams(strs []string) [][]string {
    anagramMap := make(map[string][]string)

    for _, str := range strs {
        // Convert the string to a sorted list of characters
        sortedStr := sortString(str)
        
        // Add the string to the corresponding group in the map
        anagramMap[sortedStr] = append(anagramMap[sortedStr], str)
    }

    // Collect the groups of anagrams into a result array
    result := make([][]string, 0, len(anagramMap))
    for _, group := range anagramMap {
        result = append(result, group)
    }

    return result
}

func sortString(str string) string {
    // Convert the string to a list of characters
    chars := strings.Split(str, "")
    
    // Sort the characters in ascending order
    sort.Strings(chars)
    
    // Join the sorted characters to form a string
    return strings.Join(chars, "")
}
  ```
  