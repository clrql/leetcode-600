
  # summary-ranges

  ```golang
  func summaryRanges(nums []int) []string {
	result := []string{}
	n := len(nums)
	if n == 0 {
		return result
	}

	start := nums[0]
	for i := 0; i < n; i++ {
		if i+1 < n && nums[i+1]-nums[i] == 1 {
			continue
		}

		if start == nums[i] {
			result = append(result, strconv.Itoa(start))
		} else {
			result = append(result, fmt.Sprintf("%d->%d", start, nums[i]))
		}

		if i+1 < n {
			start = nums[i+1]
		}
	}

	return result
}
  ```
  