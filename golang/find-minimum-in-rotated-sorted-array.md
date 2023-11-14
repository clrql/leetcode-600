
  # find-minimum-in-rotated-sorted-array

  ```golang
  func findMin(nums []int) int {
    return backtrack(nums, 0, len(nums)-1)
}

func backtrack(nums []int, left, right int) int {
    // If the array is not rotated, the first element is the minimum
    if nums[left] <= nums[right] {
        return nums[left]
    }

    // Binary search
    mid := left + (right-left)/2

    // Check if the mid element is the minimum
    if mid > left && nums[mid] < nums[mid-1] {
        return nums[mid]
    }

    // Check if the mid+1 element is the minimum
    if mid < right && nums[mid+1] < nums[mid] {
        return nums[mid+1]
    }

    // Recurse on the unsorted side of the array
    if nums[mid] > nums[right] {
        return backtrack(nums, mid+1, right)
    } else {
        return backtrack(nums, left, mid-1)
    }
}
  ```
  