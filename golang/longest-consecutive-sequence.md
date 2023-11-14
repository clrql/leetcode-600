
  # longest-consecutive-sequence

  ```golang
  func longestConsecutive(nums []int) int {
	if len(nums) == 0 {
		return 0
	}

	numSet := make(map[int]bool)
	for _, num := range nums {
		numSet[num] = true
	}

	longestStreak := 0

	for num := range numSet {
		// Check if the current number is the start of a sequence
		if !numSet[num-1] {
			currentNum := num
			currentStreak := 1

			// Find the length of the consecutive sequence
			for numSet[currentNum+1] {
				currentNum++
				currentStreak++
			}

			// Update the longest streak if necessary
			if currentStreak > longestStreak {
				longestStreak = currentStreak
			}
		}
	}

	return longestStreak
}

  ```
  