
  # 4sum

  ```golang
  func fourSum(nums []int, target int) [][]int {
    // sort the array
    sort.Ints(nums)
    // initialize an empty result slice
    result := [][]int{}
    
    // iterate over each number in the array
    for i := 0; i < len(nums)-3; i++ {
        // check for duplicates
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }
        // iterate over each number in the array
        for j := i+1; j < len(nums)-2; j++ {
            // check for duplicates
            if j > i+1 && nums[j] == nums[j-1] {
                continue
            }
            // initialize left and right pointers
            left := j+1
            right := len(nums)-1
            
            // move left and right pointers toward each other
            for left < right {
                // check for duplicates
                if left > j+1 && nums[left] == nums[left-1] {
                    left++
                    continue
                }
                if right < len(nums)-1 && nums[right] == nums[right+1] {
                    right--
                    continue
                }
                
                // check if current quadruplet sums to target
                sum := nums[i] + nums[j] + nums[left] + nums[right]
                if sum == target {
                    result = append(result, []int{nums[i], nums[j], nums[left], nums[right]})
                    left++
                    right--
                } else if sum < target {
                    left++
                } else {
                    right--
                }
            }
        }
    }
    return result
}

  ```
  