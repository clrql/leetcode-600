
  # contains-duplicate

  ```golang
  func containsDuplicate(nums []int) bool {
    seen := make(map[int]bool)
    
    for _, num := range nums {
        // If the number is already in the set, it's a duplicate
        if seen[num] {
            return true
        }
        // Add the number to the set
        seen[num] = true
    }
    
    return false
}

  ```
  