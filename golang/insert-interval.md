
  # insert-interval

  ```golang
  func insert(intervals [][]int, newInterval []int) [][]int {
    merged := make([][]int, 0)
    i := 0

    // Add intervals that end before the new interval starts
    for i < len(intervals) && intervals[i][1] < newInterval[0] {
        merged = append(merged, intervals[i])
        i++
    }

    // Merge overlapping intervals
    for i < len(intervals) && intervals[i][0] <= newInterval[1] {
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i++
    }

    // Add the merged interval
    merged = append(merged, newInterval)

    // Add the remaining intervals
    for i < len(intervals) {
        merged = append(merged, intervals[i])
        i++
    }

    return merged
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  