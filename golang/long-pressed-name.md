
  # long-pressed-name

  ```golang
  func isLongPressedName(name string, typed string) bool {
    i, j := 0, 0

    for j < len(typed) {
        if i < len(name) && name[i] == typed[j] {
            i++
            j++
        } else if j == 0 || typed[j] != typed[j-1] {
            return false
        } else {
            j++
        }
    }

    return i == len(name)
}
  ```
  