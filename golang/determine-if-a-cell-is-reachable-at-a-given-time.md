
  # determine-if-a-cell-is-reachable-at-a-given-time

  ```golang
  func isReachableAtTime(sx, sy, fx, fy, t int) bool {
    width := abs(sx - fx)
    height := abs(sy - fy)

    if width == 0 && height == 0 {
        return t != 1 // Handle the case where start and end are the same cell
    }

    min_time := max(width, height)

    return t >= min_time
}

func abs(x int) int {
    if x < 0 {
        return -x
    }
    return x
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  