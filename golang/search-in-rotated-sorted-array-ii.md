
  # search-in-rotated-sorted-array-ii

  ```golang
  func search(nums []int, target int) bool {
    left, right := 0, len(nums)-1

    for left <= right {
        mid := left + (right-left)/2

        if nums[mid] == target {
            return true
        }

        // Handle duplicates by moving the left or right pointer
        for left < mid && nums[left] == nums[mid] {
            left++
        }

        for mid < right && nums[mid] == nums[right] {
            right--
        }

        if nums[left] <= nums[mid] {
            // Left half is sorted
            if nums[left] <= target && target < nums[mid] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else {
            // Right half is sorted
            if nums[mid] < target && target <= nums[right] {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }

    return false
}

  ```
  