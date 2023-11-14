
  # third-maximum-number

  ```golang
  
func thirdMax(nums []int) int {
	first := math.MinInt64
	second := math.MinInt64
	third := math.MinInt64

	for _, num := range nums {
		if num == first || num == second || num == third {
			continue
		}

		if num > first {
			third = second
			second = first
			first = num
		} else if num > second {
			third = second
			second = num
		} else if num > third {
			third = num
		}
	}

	if third == math.MinInt64 {
		return first
	}

	return third
}
  ```
  