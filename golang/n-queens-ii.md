
  # n-queens-ii

  ```golang
  func totalNQueens(n int) int {
	count := 0
	columns := make([]bool, n)
	diagonal1 := make([]bool, 2*n-1)
	diagonal2 := make([]bool, 2*n-1)
	backtrack(0, n, &count, &columns, &diagonal1, &diagonal2)
	return count
}

func backtrack(row, n int, count *int, columns, diagonal1, diagonal2 *[]bool) {
	if row == n {
		*count++
		return
	}

	for col := 0; col < n; col++ {
		d1 := row - col + n - 1
		d2 := row + col

		if (*columns)[col] || (*diagonal1)[d1] || (*diagonal2)[d2] {
			continue
		}

		(*columns)[col] = true
		(*diagonal1)[d1] = true
		(*diagonal2)[d2] = true

		backtrack(row+1, n, count, columns, diagonal1, diagonal2)

		(*columns)[col] = false
		(*diagonal1)[d1] = false
		(*diagonal2)[d2] = false
	}
}
  ```
  