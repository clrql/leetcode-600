
  # determine-color-of-a-chessboard-square

  ```golang
  func squareIsWhite(coordinates string) bool {

    if int(rune(coordinates[0]) - 'a' + 1) % 2 == int(rune(coordinates[1])) % 2{
        return false
    }
    return true
}
  ```
  