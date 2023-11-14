
  # sort-array-by-parity-ii

  ```golang
  func sortArrayByParityII(nums []int) []int {
    evenIdx := 0
    oddIdx := 1
    result := make([]int, len(nums))
    for _, num := range nums {
        if num%2 == 0 {
            result[evenIdx] = num
            evenIdx += 2
        } else {
            result[oddIdx] = num
            oddIdx += 2
        }
    }
    return result
}
  ```
  