
  # intersection-of-two-arrays

  ```golang
  func intersection(nums1 []int, nums2 []int) []int {
    set := make(map[int]bool)
    intersection := []int{}
    
    // Add elements of nums1 to the set
    for _, num := range nums1 {
        set[num] = true
    }
    
    // Find intersection with nums2
    for _, num := range nums2 {
        if set[num] {
            intersection = append(intersection, num)
            set[num] = false // Remove duplicate intersections
        }
    }
    
    return intersection
}

  ```
  