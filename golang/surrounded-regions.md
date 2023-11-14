
  # surrounded-regions

  ```golang
  func solve(board [][]byte) {
    if len(board) == 0 {
        return
    }

    rows, cols := len(board), len(board[0])

    // Helper function to mark safe cells
    var markSafe func(row, col int)
    markSafe = func(row, col int) {
        if row < 0 || row >= rows || col < 0 || col >= cols || board[row][col] != 'O' {
            return
        }
        board[row][col] = 'S'
        markSafe(row-1, col) // Up
        markSafe(row+1, col) // Down
        markSafe(row, col-1) // Left
        markSafe(row, col+1) // Right
    }

    // Mark safe cells starting from the border
    for row := 0; row < rows; row++ {
        markSafe(row, 0)         // Left border
        markSafe(row, cols-1)    // Right border
    }
    for col := 1; col < cols-1; col++ {
        markSafe(0, col)         // Top border
        markSafe(rows-1, col)    // Bottom border
    }

    // Flip 'O' to 'X' and restore 'S' to 'O'
    for row := 0; row < rows; row++ {
        for col := 0; col < cols; col++ {
            if board[row][col] == 'O' {
                board[row][col] = 'X'
            } else if board[row][col] == 'S' {
                board[row][col] = 'O'
            }
        }
    }
}
  ```
  