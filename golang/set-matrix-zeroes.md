
  # set-matrix-zeroes

  ```golang
  func setZeroes(matrix [][]int) {
    m := len(matrix)
    n := len(matrix[0])

    firstRowZero := false
    firstColZero := false

    // Check if first row contains zero
    for j := 0; j < n; j++ {
        if matrix[0][j] == 0 {
            firstRowZero = true
            break
        }
    }

    // Check if first column contains zero
    for i := 0; i < m; i++ {
        if matrix[i][0] == 0 {
            firstColZero = true
            break
        }
    }

    // Mark zeros in the rest of the matrix
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            if matrix[i][j] == 0 {
                matrix[0][j] = 0
                matrix[i][0] = 0
            }
        }
    }

    // Set zeros based on marked rows and columns
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            if matrix[0][j] == 0 || matrix[i][0] == 0 {
                matrix[i][j] = 0
            }
        }
    }

    // Set zeros in the first row if necessary
    if firstRowZero {
        for j := 0; j < n; j++ {
            matrix[0][j] = 0
        }
    }

    // Set zeros in the first column if necessary
    if firstColZero {
        for i := 0; i < m; i++ {
            matrix[i][0] = 0
        }
    }
}

  ```
  