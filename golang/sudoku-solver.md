
  # sudoku-solver

  ```golang
  func solveSudoku(board [][]byte) {
    solve(board, 0, 0)
}

func solve(board [][]byte, row, col int) bool {
    if row == 9 {
        return true
    }
    if col == 9 {
        return solve(board, row+1, 0)
    }
    if board[row][col] != '.' {
        return solve(board, row, col+1)
    }
    for num := '1'; num <= '9'; num++ {
        if isValid(board, row, col, byte(num)) {
            board[row][col] = byte(num)
            if solve(board, row, col+1) {
                return true
            }
            board[row][col] = '.'
        }
    }
    return false
}

func isValid(board [][]byte, row, col int, c byte) bool {
    for i := 0; i < 9; i++ {
        if board[row][i] == c || board[i][col] == c || board[3*(row/3)+i/3][3*(col/3)+i%3] == c {
            return false
        }
    }
    return true
}
  ```
  