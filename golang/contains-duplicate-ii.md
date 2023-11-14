
  # contains-duplicate-ii

  ```golang
  func containsNearbyDuplicate(nums []int, k int) bool {
    numIndex := make(map[int]int) // Map to store the indices of encountered numbers
    
    for i, num := range nums {
        if j, ok := numIndex[num]; ok && i-j <= k {
            return true
        }
        numIndex[num] = i // Update the index of the number
    }
    
    return false
}

  ```
  