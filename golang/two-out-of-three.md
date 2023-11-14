
  # two-out-of-three

  ```golang
  func twoOutOfThree(nums1 []int, nums2 []int, nums3 []int) []int {
    hash := make(map[int]int)
    result := []int{}

    addToMap := func(nums []int) {
        unique := make(map[int]bool)
        for _, num := range nums {
            unique[num] = true
        }

        for num := range unique {
            hash[num]++
        }
    }

    addToMap(nums1)
    addToMap(nums2)
    addToMap(nums3)

    for num, count := range hash {
        if (count >= 2) {
            result = append(result, num)
        }
    }

    return result
}
  ```
  