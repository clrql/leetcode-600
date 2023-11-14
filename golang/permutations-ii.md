
  # permutations-ii

  ```golang
  func permuteUnique(nums []int) [][]int {
    var result [][]int
    var current []int
    used := make([]bool, len(nums))
    sort.Ints(nums) // Sort the input to handle duplicates easily
    backtrack(nums, used, current, &result)
    return result
}

func backtrack(nums []int, used []bool, current []int, result *[][]int) {
    if len(current) == len(nums) {
        // Create a copy of the current permutation to avoid modifying it later
        temp := make([]int, len(current))
        copy(temp, current)
        *result = append(*result, temp)
        return
    }

    for i := 0; i < len(nums); i++ {
        if used[i] || (i > 0 && nums[i] == nums[i-1] && !used[i-1]) {
            // Skip duplicates and already used numbers
            continue
        }
        used[i] = true
        current = append(current, nums[i])
        backtrack(nums, used, current, result)
        used[i] = false
        current = current[:len(current)-1]
    }
}
  ```
  