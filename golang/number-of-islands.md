
  # number-of-islands

  ```golang
  func numIslands(grid [][]byte) int {
	if len(grid) == 0 || len(grid[0]) == 0 {
		return 0
	}

	numRows, numCols := len(grid), len(grid[0])
	count := 0

	var stack [][]int

	for i := 0; i < numRows; i++ {
		for j := 0; j < numCols; j++ {
			if grid[i][j] == '1' {
				count++
				stack = append(stack, []int{i, j})

				for len(stack) > 0 {
					curr := stack[len(stack)-1]
					stack = stack[:len(stack)-1]
					row, col := curr[0], curr[1]

					if row < 0 || row >= numRows || col < 0 || col >= numCols || grid[row][col] != '1' {
						continue
					}

					grid[row][col] = '0'

					stack = append(stack, []int{row - 1, col})
					stack = append(stack, []int{row + 1, col})
					stack = append(stack, []int{row, col - 1})
					stack = append(stack, []int{row, col + 1})
				}
			}
		}
	}

	return count
}
  ```
  