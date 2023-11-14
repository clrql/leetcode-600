
  # valid-boomerang

  ```golang
  func isBoomerang(points [][]int) bool {
    // Check if the points are distinct
    if points[0][0] == points[1][0] && points[0][1] == points[1][1] ||
        points[0][0] == points[2][0] && points[0][1] == points[2][1] ||
        points[1][0] == points[2][0] && points[1][1] == points[2][1] {
        return false
    }

    // Check if the slopes of two lines are not equal
    return (points[0][1]-points[1][1])*(points[0][0]-points[2][0]) != (points[0][1]-points[2][1])*(points[0][0]-points[1][0])
}

  ```
  