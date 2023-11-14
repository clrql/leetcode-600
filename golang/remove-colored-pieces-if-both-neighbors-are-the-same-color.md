
  # remove-colored-pieces-if-both-neighbors-are-the-same-color

  ```golang
  func winnerOfGame(colors string) bool {
    countA := 0
    countB := 0

    for i := 0; i < len(colors); i++ {
        x := colors[i]
        count := 0

        for i < len(colors) && colors[i] == x {
            i++
            count++
        }

        if x == 'A' {
            countA += max(count-2, 0)
        } else if x == 'B' {
            countB += max(count-2, 0)
        }

        i--
    }

    return countA > countB
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
  ```
  