
  # merge-sorted-array

  ```golang
  func merge(nums1 []int, m int, nums2 []int, n int) {
    // Start merging from the end of the merged array
    i := m - 1
    j := n - 1
    k := m + n - 1

    // Merge nums1 and nums2 from the end
    for i >= 0 && j >= 0 {
        if nums1[i] > nums2[j] {
            nums1[k] = nums1[i]
            i--
        } else {
            nums1[k] = nums2[j]
            j--
        }
        k--
    }

    // Copy remaining elements from nums2 to nums1
    for j >= 0 {
        nums1[k] = nums2[j]
        j--
        k--
    }
}

  ```
  