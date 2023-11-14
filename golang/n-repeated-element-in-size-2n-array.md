
  # n-repeated-element-in-size-2n-array

  ```golang
  func repeatedNTimes(nums []int) int {
    freqMap := make(map[int]int)

    for _, num := range nums {
        freqMap[num]++
        if freqMap[num] == len(nums)/2 {
            return num
        }
    }

    return 0 // Return 0 if no repeated element is found (which shouldn't happen based on the problem constraints).
}

  ```
  