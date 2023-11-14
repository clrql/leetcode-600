
  # image-smoother

  ```golang
  func imageSmoother(img [][]int) [][]int {
    m, n := len(img), len(img[0])
    result := make([][]int, m)
    for i := range result {
        result[i] = make([]int, n)
    }

    directions := []int{-1, 0, 1}

    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            sum := 0
            count := 0

            for _, dx := range directions {
                for _, dy := range directions {
                    ni, nj := i+dx, j+dy
                    if ni >= 0 && ni < m && nj >= 0 && nj < n {
                        sum += img[ni][nj]
                        count++
                    }
                }
            }

            result[i][j] = sum / count
        }
    }

    return result
}

  ```
  