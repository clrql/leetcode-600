
  # valid-sudoku

  ```golang
  func isValidSudoku(board [][]byte) bool {
    // Create sets to track digits in each row, column, and sub-grid
	rows := make([]map[byte]bool, 9)
	cols := make([]map[byte]bool, 9)
	grids := make([]map[byte]bool, 9)

	for i := 0; i < 9; i++ {
		rows[i] = make(map[byte]bool)
		cols[i] = make(map[byte]bool)
		grids[i] = make(map[byte]bool)
	}

	for i := 0; i < 9; i++ {
		for j := 0; j < 9; j++ {
			digit := board[i][j]

			if digit == '.' {
				continue // Skip empty cells
			}

			// Check row
			if rows[i][digit] {
				return false
			}
			rows[i][digit] = true

			// Check column
			if cols[j][digit] {
				return false
			}
			cols[j][digit] = true

			// Check sub-grid
			gridIdx := (i/3)*3 + j/3
			if grids[gridIdx][digit] {
				return false
			}
			grids[gridIdx][digit] = true
		}
	}

	return true
}
  ```
  