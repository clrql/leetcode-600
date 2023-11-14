
  # find-the-town-judge

  ```golang
  func findJudge(n int, trust [][]int) int {
    // Initialize arrays to count trusts given and received
    trustGiven := make([]int, n+1)
    trustReceived := make([]int, n+1)

    for _, relation := range trust {
        a, b := relation[0], relation[1]
        trustGiven[a]++
        trustReceived[b]++
    }

    for i := 1; i <= n; i++ {
        if trustReceived[i] == n-1 && trustGiven[i] == 0 {
            return i
        }
    }

    return -1
}

  ```
  