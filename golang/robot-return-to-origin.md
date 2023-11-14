
  # robot-return-to-origin

  ```golang
  func judgeCircle(moves string) bool {
    x, y := 0, 0
    for _, move := range moves {
        switch move {
            case 'U':
                y++
            case 'D':
                y--
            case 'L':
                x--
            case 'R':
                x++
        }
    }
    return x == 0 && y == 0
}
  ```
  