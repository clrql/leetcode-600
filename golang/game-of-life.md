
  # game-of-life

  ```golang
  func gameOfLife(board [][]int) {
	m := len(board)
	n := len(board[0])

	// Helper function to count live neighbors
	countLiveNeighbors := func(row, col int) int {
		count := 0
		for i := row - 1; i <= row+1; i++ {
			for j := col - 1; j <= col+1; j++ {
				if i >= 0 && i < m && j >= 0 && j < n && !(i == row && j == col) {
					count += board[i][j] & 1
				}
			}
		}
		return count
	}

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			liveNeighbors := countLiveNeighbors(i, j)
			if board[i][j] == 1 && (liveNeighbors == 2 || liveNeighbors == 3) {
				// Live cell with 2 or 3 live neighbors survives
				board[i][j] = 3
			}
			if board[i][j] == 0 && liveNeighbors == 3 {
				// Dead cell with 3 live neighbors becomes alive
				board[i][j] = 2
			}
		}
	}

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			// Update the board with the next state
			board[i][j] >>= 1
		}
	}
}

  ```
  