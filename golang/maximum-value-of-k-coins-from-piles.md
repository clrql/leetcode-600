
  # maximum-value-of-k-coins-from-piles

  ```golang
  func maxValueOfCoins(piles [][]int, k int) int {
	memo := make([][]int, len(piles)+1)
	for i := range memo {
		memo[i] = make([]int, k+1)
	}

	return dp(piles, memo, 0, k)
}

func dp(piles [][]int, memo [][]int, i int, k int) int {
	if k == 0 || i == len(piles) {
		return 0
	}
	if memo[i][k] != 0 {
		return memo[i][k]
	}

	res := dp(piles, memo, i+1, k)
	cur := 0

	for j := 0; j < min(len(piles[i]), k); j++ {
		cur += piles[i][j]
		res = max(res, cur+dp(piles, memo, i+1, k-j-1))
	}

	memo[i][k] = res
	return res
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
  