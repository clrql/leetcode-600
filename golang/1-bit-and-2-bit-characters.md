
  # 1-bit-and-2-bit-characters

  ```golang
  func isOneBitCharacter(bits []int) bool {
    i := 0
    for i < len(bits)-1 {
        if bits[i] == 0 {
            i++
        } else {
            i += 2
        }
    }
    return i == len(bits)-1
}

  ```
  