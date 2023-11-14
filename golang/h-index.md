
  # h-index

  ```golang
  func hIndex(citations []int) int {
    n := len(citations)
    count := make([]int, n+1)

    // Count the number of papers for each citation
    for _, citation := range citations {
        if citation > n {
            count[n]++
        } else {
            count[citation]++
        }
    }

    // Calculate the h-index
    hIndex := 0
    papers := 0
    for i := n; i >= 0; i-- {
        papers += count[i]
        if papers >= i {
            hIndex = i
            break
        }
    }

    return hIndex
}

  ```
  