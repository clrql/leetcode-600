
  # partition-labels

  ```golang
  func partitionLabels(s string) []int {
	// Store the last occurrence index of each character
	lastIndex := make(map[byte]int)
	for i := 0; i < len(s); i++ {
		lastIndex[s[i]] = i
	}

	partitionSizes := make([]int, 0)
	start := 0
	end := 0

	for i := 0; i < len(s); i++ {
		// Update the end index to the maximum of current end and the last occurrence index of the current character
		end = max(end, lastIndex[s[i]])

		// If the current index reaches the end index, we have found a partition
		if i == end {
			partitionSizes = append(partitionSizes, end-start+1)
			start = end + 1
		}
	}

	return partitionSizes
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
  ```
  