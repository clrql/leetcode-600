
  # binary-watch

  ```golang
  func readBinaryWatch(turnedOn int) []string {
	var result []string

	for hour := 0; hour < 12; hour++ {
		for minute := 0; minute < 60; minute++ {
			if countBits(hour)+countBits(minute) == turnedOn {
				timeStr := fmt.Sprintf("%d:%02d", hour, minute)
				result = append(result, timeStr)
			}
		}
	}

	return result
}

func countBits(num int) int {
	count := 0
	for num > 0 {
		if num&1 == 1 {
			count++
		}
		num >>= 1
	}
	return count
}
  ```
  