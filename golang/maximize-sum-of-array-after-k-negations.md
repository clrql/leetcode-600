
  # maximize-sum-of-array-after-k-negations

  ```golang
  import "sort"

func largestSumAfterKNegations(nums []int, k int) int {
    // Sort the array in ascending order
    sort.Ints(nums)

    i := 0
    for k > 0 && i < len(nums) && nums[i] < 0 {
        // Negate the current element
        nums[i] = -nums[i]
        i++
        k--
    }

    // If k is still greater than 0 and is odd, negate the smallest element
    if k%2 == 1 {
        // Find the index of the smallest element
        minIdx := 0
        for j := 1; j < len(nums); j++ {
            if nums[j] < nums[minIdx] {
                minIdx = j
            }
        }
        // Negate the smallest element
        nums[minIdx] = -nums[minIdx]
    }

    // Calculate the sum of the modified array
    sum := 0
    for _, num := range nums {
        sum += num
    }

    return sum
}

  ```
  