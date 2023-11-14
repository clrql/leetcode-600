
  # word-search

  ```golang
  func exist(board [][]byte, word string) bool {
    rows := len(board)
    cols := len(board[0])
    
    // Create a visited array to keep track of visited cells
    visited := make([][]bool, rows)
    for i := 0; i < rows; i++ {
        visited[i] = make([]bool, cols)
    }
    
    // Iterate through each cell and check if the word exists
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if board[i][j] == word[0] && backtrack(board, word, visited, i, j, 0) {
                return true
            }
        }
    }
    
    return false
}

func backtrack(board [][]byte, word string, visited [][]bool, row, col, index int) bool {
    // Check if all characters in the word have been found
    if index == len(word) {
        return true
    }
    
    // Check if the current cell is out of bounds or has been visited
    if row < 0 || row >= len(board) || col < 0 || col >= len(board[0]) || visited[row][col] {
        return false
    }
    
    // Check if the current cell matches the character in the word
    if board[row][col] != word[index] {
        return false
    }
    
    // Mark the current cell as visited
    visited[row][col] = true
    
    // Explore the neighboring cells in a recursive manner
    found := backtrack(board, word, visited, row-1, col, index+1) ||
        backtrack(board, word, visited, row+1, col, index+1) ||
        backtrack(board, word, visited, row, col-1, index+1) ||
        backtrack(board, word, visited, row, col+1, index+1)
    
    // Mark the current cell as unvisited for future backtracking
    visited[row][col] = false
    
    return found
}

  ```
  