
  # distribute-candies-to-people

  ```golang
  func distributeCandies(candies int, num_people int) []int {
    ans := make([]int, num_people)
    turn := 0

    for candies > 0 {
        for i := 0; i < num_people; i++ {
            giveCandies := min(candies, turn*num_people+i+1)
            ans[i] += giveCandies
            candies -= giveCandies

            if candies <= 0 {
                break
            }
        }
        turn++
    }

    return ans
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

  ```
  