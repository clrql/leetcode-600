
  # spiral-matrix

  ```golang
  func spiralOrder(matrix [][]int) []int {
    if len(matrix) == 0 {
        return []int{}
    }
    
    var result []int
    rowStart, rowEnd := 0, len(matrix)-1
    colStart, colEnd := 0, len(matrix[0])-1
    
    for rowStart <= rowEnd && colStart <= colEnd {
        // Traverse right
        for j := colStart; j <= colEnd; j++ {
            result = append(result, matrix[rowStart][j])
        }
        rowStart++
        
        // Traverse down
        for i := rowStart; i <= rowEnd; i++ {
            result = append(result, matrix[i][colEnd])
        }
        colEnd--
        
        // Traverse left
        if rowStart <= rowEnd {
            for j := colEnd; j >= colStart; j-- {
                result = append(result, matrix[rowEnd][j])
            }
            rowEnd--
        }
        
        // Traverse up
        if colStart <= colEnd {
            for i := rowEnd; i >= rowStart; i-- {
                result = append(result, matrix[i][colStart])
            }
            colStart++
        }
    }
    
    return result
}

  ```
  