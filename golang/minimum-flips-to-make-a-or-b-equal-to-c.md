
  # minimum-flips-to-make-a-or-b-equal-to-c

  ```golang
  func minFlips(a int, b int, c int) int {
    flips := 0
    for i := 0; i < 32; i++ {
        bitA := (a >> i) & 1
        bitB := (b >> i) & 1
        bitC := (c >> i) & 1
        
        if bitC == 0 {
            if bitA == 1 {
                flips++
            }
            if bitB == 1 {
                flips++
            }
        } else {
            if bitA == 0 && bitB == 0 {
                flips++
            }
        }
    }
    return flips
}
  ```
  