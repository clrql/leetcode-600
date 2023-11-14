
  # surface-area-of-3d-shapes

  ```golang
  func surfaceArea(grid [][]int) int {
    n := len(grid)
    surface := 0

    for i := 0; i < n; i++ {
        for j := 0; j < n; j++ {
            if grid[i][j] > 0 {
                surface += (grid[i][j] * 4) + 2
                if i > 0 {
                    surface -= min(grid[i][j], grid[i - 1][j]) * 2;
                }
                if j > 0 {
                    surface -= min(grid[i][j], grid[i][j - 1]) * 2;
                }
            }
        }
    }

    return surface
}

func min(a int, b int) int {
    if a < b {
        return a
    }
    return b
}
  ```
  