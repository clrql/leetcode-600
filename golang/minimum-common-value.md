
  # minimum-common-value

  ```golang
  // enfoque meh
/*
func getCommon(nums1 []int, nums2 []int) int {
    for _, i := range nums1 {
        for _, j := range nums2 {
            if i == j {
                return i
            }
        }
    }
    return -1
}
*/

// enfoque de dos punteros
/*
func getCommon(nums1 []int, nums2 []int) int {
    i, j := 0, 0
    for i < len(nums1) && j < len(nums2) {
        switch {
        case nums1[i] == nums2[j]:
            return nums1[i]
        case nums1[i] < nums2[j]:
            i++
        default:
            j++
        }
    }
    return -1
}
*/

func getCommon(nums1 []int, nums2 []int) int {
    hash := make(map[int]int, len(nums2))

    for i, num := range nums2 {
        hash[num] = i
    }

    for _, num := range nums1 {
        _, ok := hash[num]
        if ok {
            return num
        }
    }

    return -1
}
  ```
  