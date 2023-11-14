
  # 3sum

  ```golang
  func threeSum(nums []int) [][]int {
    // sort the array
    sort.Ints(nums)
    // initialize an empty result slice
    result := [][]int{}
    
    // iterate over each number in the array
    for i := 0; i < len(nums)-2; i++ {
        // check for duplicates
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }
        // initialize left and right pointers
        left := i+1
        right := len(nums)-1
        
        // move left and right pointers toward each other
        for left < right {
            // check for duplicates
            if left > i+1 && nums[left] == nums[left-1] {
                left++
                continue
            }
            if right < len(nums)-1 && nums[right] == nums[right+1] {
                right--
                continue
            }
            
            // check if current triplet sums to 0
            sum := nums[i] + nums[left] + nums[right]
            if sum == 0 {
                result = append(result, []int{nums[i], nums[left], nums[right]})
                left++
                right--
            } else if sum < 0 {
                left++
            } else {
                right--
            }
        }
    }
    return result
}

  ```
  