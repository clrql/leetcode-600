
  # can-place-flowers

  ```golang
  func canPlaceFlowers(flowerbed []int, n int) bool {
    count := 0
    length := len(flowerbed)
    for i := 0; i < length && count < n; i++ {
        if flowerbed[i] == 0 && (i == 0 || flowerbed[i-1] == 0) && (i == length-1 || flowerbed[i+1] == 0) {
            flowerbed[i] = 1
            count++
        }
    }
    return count >= n
}
  ```
  