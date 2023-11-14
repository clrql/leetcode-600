
  # find-all-numbers-disappeared-in-an-array

  ```golang
  func findDisappearedNumbers(nums []int) []int {
    n := len(nums)
    if n == 0 { return nil }
    res := make([]int, n)
    for _, num := range nums {
        res[num-1] = num
    }
    j := 0
    for i := 0; i < n; i++ {
        if res[i] == 0 {
            res[j] = i + 1
            j++
        }
    }
    return res[:j]
}
  ```
  