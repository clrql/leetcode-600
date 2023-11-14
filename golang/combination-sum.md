
  # combination-sum

  ```golang
  func combinationSum(candidates []int, target int) [][]int {
    // Step 1: Sort candidates array
    sort.Ints(candidates)

    // Step 2: Initialize result array
    result := [][]int{}

    // Step 5: Call backtrack function
    backtrack(&result, []int{}, candidates, target, 0)

    // Step 6: Return result array
    return result
}

// Step 3: Define backtrack function
func backtrack(result *[][]int, combination []int, candidates []int, target int, start int) {
    // Step 4a: Check if sum equals target
    if target == 0 {
        // Append a copy of the combination to the result
        temp := make([]int, len(combination))
        copy(temp, combination)
        *result = append(*result, temp)
        return
    }

    // Step 4b: Check if sum exceeds target or index out of bounds
    if target < 0 || start >= len(candidates) {
        return
    }

    // Step 4c: Iterate over candidates
    for i := start; i < len(candidates); i++ {
        candidate := candidates[i]

        // Add candidate to the combination
        combination = append(combination, candidate)

        // Step 4c: Recursively call backtrack with updated combination, sum, and index
        backtrack(result, combination, candidates, target-candidate, i)

        // Remove last candidate from the combination
        combination = combination[:len(combination)-1]
    }
}
  ```
  