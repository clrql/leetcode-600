
  # merge-intervals

  ```golang
  func merge(intervals [][]int) [][]int {
	if len(intervals) <= 1 {
		return intervals
	}

	// Sort intervals based on the start time
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i][0] < intervals[j][0]
	})

	result := make([][]int, 0)
	currentInterval := intervals[0]

	for i := 1; i < len(intervals); i++ {
		if intervals[i][0] <= currentInterval[1] {
			// Merge the overlapping intervals
			currentInterval[1] = max(currentInterval[1], intervals[i][1])
		} else {
			// Add the non-overlapping interval to the result
			result = append(result, currentInterval)
			currentInterval = intervals[i]
		}
	}

	// Add the last interval to the result
	result = append(result, currentInterval)

	return result
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
  ```
  