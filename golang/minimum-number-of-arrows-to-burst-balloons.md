
  # minimum-number-of-arrows-to-burst-balloons

  ```golang
  func findMinArrowShots(points [][]int) int {
	// Sort the balloons based on their end coordinates
	sort.Slice(points, func(i, j int) bool {
		return points[i][1] < points[j][1]
	})

	// Initialize the number of arrows and the end coordinate of the current arrow
	arrows := 0
	end := points[0][1]

	// Iterate through the sorted balloons
	for i := 1; i < len(points); i++ {
		// If the balloon's start coordinate is greater than the current arrow's end coordinate,
		// it means we need an additional arrow since the previous arrow cannot burst this balloon.
		if points[i][0] > end {
			arrows++
			end = points[i][1]
		}
	}

	// Return the minimum number of arrows needed
	return arrows + 1
}

  ```
  