
  # n-queens

  ```golang
  func solveNQueens(n int) [][]string {
    res := [][]string{}
    cols, diags1, diags2 := make(map[int]bool), make(map[int]bool), make(map[int]bool)
    board := make([]string, n)
    for i := range board {
        board[i] = strings.Repeat(".", n)
    }
    backtrack(0, board, &res, cols, diags1, diags2, n)
    return res
}

func backtrack(row int, board []string, res *[][]string, cols, diags1, diags2 map[int]bool, n int) {
    if row == n {
        tmp := make([]string, n)
        copy(tmp, board)
        *res = append(*res, tmp)
        return
    }
    for col := 0; col < n; col++ {
        if !cols[col] && !diags1[row-col] && !diags2[row+col] {
            cols[col], diags1[row-col], diags2[row+col] = true, true, true
            board[row] = board[row][:col] + "Q" + board[row][col+1:]
            backtrack(row+1, board, res, cols, diags1, diags2, n)
            cols[col], diags1[row-col], diags2[row+col] = false, false, false
            board[row] = board[row][:col] + "." + board[row][col+1:]
        }
    }
}

  ```
  