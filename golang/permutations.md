
  # permutations

  ```golang
  func permute(nums []int) [][]int {
    permutations := [][]int{}

    backtrack(nums, &permutations, 0)

    return permutations
}

func backtrack(nums []int, permutations *[][]int, start int) {
    if start == len(nums) {
        currentPermutation := make([]int, len(nums))
        copy(currentPermutation, nums)
        *permutations = append(*permutations, currentPermutation)
        return
    }

    for i := start; i < len(nums); i++ {
        nums[start], nums[i] = nums[i], nums[start]

        backtrack(nums, permutations, start+1)

        nums[start], nums[i] = nums[i], nums[start]
    }

}
  ```
  