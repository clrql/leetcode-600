
  # find-the-winner-of-an-array-game

  ```golang
  func getWinner(arr []int, k int) int {
    maxNum := arr[0]
    consecutiveWins := 0

    for i := 1; i < len(arr); i++ {
        if arr[i] > maxNum {
            maxNum = arr[i]
            consecutiveWins = 1
        } else {
            consecutiveWins++
        }

        if consecutiveWins == k {
            return maxNum
        }

        if i == len(arr)-1 {
            i = 0 // Restart the game if no winner in a round
        }
    }

    return maxNum
}

  ```
  