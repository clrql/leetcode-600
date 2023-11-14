
  # subsets-ii

  ```golang
  func subsetsWithDup(nums []int) [][]int {
    // Sort the input array to handle duplicates
    sort.Ints(nums)

    subsets := make([][]int, 0)
    subset := make([]int, 0)

    var backtrack func(start int)
    backtrack = func(start int) {
        subsetCopy := make([]int, len(subset))
        copy(subsetCopy, subset)
        subsets = append(subsets, subsetCopy)

        for i := start; i < len(nums); i++ {
            // Skip duplicates
            if i > start && nums[i] == nums[i-1] {
                continue
            }

            subset = append(subset, nums[i])
            backtrack(i + 1)
            subset = subset[:len(subset)-1]
        }
    }

    backtrack(0)
    return subsets
}

  ```
  