
  # last-moment-before-all-ants-fall-out-of-a-plank

  ```golang
  func getLastMoment(n int, left []int, right []int) int {
    lastMoment := 0

    for _, pos := range left {
        lastMoment = max(lastMoment, pos)
    }

    for _, pos := range right {
        lastMoment = max(lastMoment, n-pos)
    }

    return lastMoment
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  