
  # degree-of-an-array

  ```golang
  func findShortestSubArray(nums []int) int {
    count := make(map[int][]int)

    for i, num := range nums {
        if _, ok := count[num]; !ok {
            count[num] = []int{1, i, i}
        } else {
            count[num][0]++
            count[num][2] = i
        }
    }

    degree := 0
    minLength := 0

    for _, c := range count {
        if c[0] > degree {
            degree = c[0]
            minLength = c[2] - c[1] + 1
        } else if c[0] == degree {
            minLength = min(minLength, c[2]-c[1]+1)
        }
    }

    return minLength
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

  ```
  