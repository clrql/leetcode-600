
  # find-the-k-or-of-an-array

  ```golang
  func findKOr(nums []int, k int) int {
    maxBit := 32 // Considering integers are 32-bit
	result := 0

	for i := 0; i < maxBit; i++ {
		if countBitsSet(nums, i) >= k {
			result |= 1 << i
		}
	}

	return result
}

func countBitsSet(nums []int, bit int) int {
	count := 0
	for _, num := range nums {
		if num&(1<<bit) != 0 {
			count++
		}
	}
	return count
}
  ```
  