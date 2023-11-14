
  # combinations

  ```golang
  func combine(n int, k int) [][]int {
	result := [][]int{}
	current := []int{}

	backtrack(&result, current, 1, n, k)

	return result
}

func backtrack(result *[][]int, current []int, start, n, k int) {
	if len(current) == k {
		combination := make([]int, k)
		copy(combination, current)
		*result = append(*result, combination)
		return
	}

	for i := start; i <= n; i++ {
		current = append(current, i)
		backtrack(result, current, i+1, n, k)
		current = current[:len(current)-1]
	}
}
  ```
  