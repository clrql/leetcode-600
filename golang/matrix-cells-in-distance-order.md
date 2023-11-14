
  # matrix-cells-in-distance-order

  ```golang
  import "math"

func allCellsDistOrder(rows int, cols int, rCenter int, cCenter int) [][]int {
    result := make([][]int, rows*cols)
    index := 0

    for r := 0; r < rows; r++ {
        for c := 0; c < cols; c++ {
            result[index] = []int{r, c}
            index++
        }
    }

    // Sort the cells based on their distance from the center cell
    sort.Slice(result, func(i, j int) bool {
        dist1 := int(math.Abs(float64(result[i][0]-rCenter))) + int(math.Abs(float64(result[i][1]-cCenter)))
        dist2 := int(math.Abs(float64(result[j][0]-rCenter))) + int(math.Abs(float64(result[j][1]-cCenter)))
        return dist1 < dist2
    })

    return result
}

  ```
  