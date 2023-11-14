
  # largest-number-at-least-twice-of-others

  ```golang
  func dominantIndex(nums []int) int {
    n := len(nums)
    if n == 1 {
        return 0
    }

    largest := 0
    secondLargest := -1

    for i := 1; i < n; i++ {
        if nums[i] > nums[largest] {
            secondLargest = largest
            largest = i
        } else if secondLargest == -1 || nums[i] > nums[secondLargest] {
            secondLargest = i
        }
    }

    if nums[largest] >= 2*nums[secondLargest] {
        return largest
    }
    return -1
}

  ```
  