
  # number-of-increasing-paths-in-a-grid

  ```golang
  func countPaths(grid [][]int) int {
	m, n := len(grid), len(grid[0])
	ans, mod := 0, 1000000007
	dp := make([][]int, m)
	for i := 0; i < m; i++ {
		dp[i] = make([]int, n)
		for j := 0; j < n; j++ {
			dp[i][j] = -1
		}
	}

	var dfs func(int, int) int
	dfs = func(r, c int) int {
		if dp[r][c] != -1 {
			return dp[r][c]
		}
		cellValue := 1
		direction := [4][2]int{{r - 1, c}, {r, c + 1}, {r + 1, c}, {r, c - 1}}
		for _, d := range direction {
			nr, nc := d[0], d[1]
			if 0 <= nr && nr < m && 0 <= nc && nc < n && grid[nr][nc] > grid[r][c] {
				cellValue = (cellValue%mod + dfs(nr, nc)%mod) % mod
			}
		}
		dp[r][c] = cellValue
		return dp[r][c]
	}

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			ans = (ans%mod + dfs(i, j)%mod) % mod
		}
	}
	return ans
}
  ```
  