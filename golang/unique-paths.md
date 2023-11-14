
  # unique-paths

  ```golang
  func uniquePaths(m int, n int) int {
    // Create a 2D grid to store the number of paths for each cell
    grid := make([][]int, m)
    for i := 0; i < m; i++ {
        grid[i] = make([]int, n)
    }
    
    // Set the number of paths for the first row and first column to 1
    for i := 0; i < m; i++ {
        grid[i][0] = 1
    }
    for j := 0; j < n; j++ {
        grid[0][j] = 1
    }
    
    // Calculate the number of paths for each cell based on the previous cells
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            grid[i][j] = grid[i-1][j] + grid[i][j-1]
        }
    }
    
    // Return the number of paths for the bottom-right cell
    return grid[m-1][n-1]
}

  ```
  