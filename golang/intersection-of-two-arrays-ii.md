
  # intersection-of-two-arrays-ii

  ```golang
  func intersect(nums1 []int, nums2 []int) []int {
    freq := make(map[int]int)
    intersection := []int{}
    
    // Count frequencies of elements in nums1
    for _, num := range nums1 {
        freq[num]++
    }
    
    // Find intersection with nums2 while considering frequencies
    for _, num := range nums2 {
        if freq[num] > 0 {
            intersection = append(intersection, num)
            freq[num]--
        }
    }
    
    return intersection
}

  ```
  