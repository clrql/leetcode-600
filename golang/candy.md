
  # candy

  ```golang
  func candy(ratings []int) int {
    n := len(ratings)
    candies := make([]int, n)

    // Initialize candies array with 1 candy for each child
    for i := 0; i < n; i++ {
        candies[i] = 1
    }

    // Traverse from left to right, assign more candies to higher-rated children
    for i := 1; i < n; i++ {
        if ratings[i] > ratings[i-1] {
            candies[i] = candies[i-1] + 1
        }
    }

    // Traverse from right to left, make sure neighbors with higher rating have more candies
    for i := n - 2; i >= 0; i-- {
        if ratings[i] > ratings[i+1] && candies[i] <= candies[i+1] {
            candies[i] = candies[i+1] + 1
        }
    }

    // Calculate the total number of candies needed
    totalCandies := 0
    for _, num := range candies {
        totalCandies += num
    }

    return totalCandies
}

  ```
  