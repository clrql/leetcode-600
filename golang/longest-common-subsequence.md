
  # longest-common-subsequence

  ```golang
  func longestCommonSubsequence(text1 string, text2 string) int {
    m := len(text1)
    n := len(text2)
    
    // Create a 2D grid to store the lengths of longest common subsequences
    grid := make([][]int, m+1)
    for i := 0; i <= m; i++ {
        grid[i] = make([]int, n+1)
    }
    
    // Calculate the lengths of longest common subsequences
    for i := 1; i <= m; i++ {
        for j := 1; j <= n; j++ {
            if text1[i-1] == text2[j-1] {
                grid[i][j] = grid[i-1][j-1] + 1
            } else {
                grid[i][j] = max(grid[i-1][j], grid[i][j-1])
            }
        }
    }
    
    // Return the length of the longest common subsequence
    return grid[m][n]
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  