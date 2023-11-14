
  # available-captures-for-rook

  ```golang
  func numRookCaptures(board [][]byte) int {
    var rookRow, rookCol int

    // Find the position of the white rook 'R'
    for i := 0; i < 8; i++ {
        for j := 0; j < 8; j++ {
            if board[i][j] == 'R' {
                rookRow, rookCol = i, j
                break
            }
        }
    }

    // Define the four cardinal directions (north, east, south, west)
    directions := [][2]int{{-1, 0}, {0, 1}, {1, 0}, {0, -1}}

    captures := 0

    for _, direction := range directions {
        row, col := rookRow, rookCol

        // Simulate rook's movement in the current direction
        for {
            row += direction[0]
            col += direction[1]

            // Check if the rook is out of the board or blocked by a white bishop 'B'
            if row < 0 || row >= 8 || col < 0 || col >= 8 || board[row][col] == 'B' {
                break
            }

            // Check if the rook captures a black pawn 'p'
            if board[row][col] == 'p' {
                captures++
                break
            }
        }
    }

    return captures
}

  ```
  