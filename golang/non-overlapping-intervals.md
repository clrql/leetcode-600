
  # non-overlapping-intervals

  ```golang
  func eraseOverlapIntervals(intervals [][]int) int {
	if len(intervals) == 0 {
		return 0
	}

	// Sort intervals based on their end coordinates
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i][1] < intervals[j][1]
	})

	// Initialize variables
	end := intervals[0][1]
	removals := 0

	// Iterate through intervals
	for i := 1; i < len(intervals); i++ {
		// If the start of the current interval is less than the end of the previous interval,
		// it means there is an overlap and we need to remove one interval.
		if intervals[i][0] < end {
			removals++
		} else {
			end = intervals[i][1]
		}
	}

	return removals
}

  ```
  