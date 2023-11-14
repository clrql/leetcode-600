
  # spiral-matrix-ii

  ```golang
  func generateMatrix(n int) [][]int {
    // Initialize the result matrix with all zeros.
    matrix := make([][]int, n)
    for i := 0; i < n; i++ {
        matrix[i] = make([]int, n)
    }

    num := 1
    top, bottom, left, right := 0, n-1, 0, n-1

    for num <= n*n {
        // Fill the top row.
        for i := left; i <= right; i++ {
            matrix[top][i] = num
            num++
        }
        top++

        // Fill the rightmost column.
        for i := top; i <= bottom; i++ {
            matrix[i][right] = num
            num++
        }
        right--

        // Fill the bottom row.
        for i := right; i >= left; i-- {
            matrix[bottom][i] = num
            num++
        }
        bottom--

        // Fill the leftmost column.
        for i := bottom; i >= top; i-- {
            matrix[i][left] = num
            num++
        }
        left++
    }

    return matrix
}

  ```
  