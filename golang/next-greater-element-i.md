
  # next-greater-element-i

  ```golang
  func nextGreaterElement(nums1 []int, nums2 []int) []int {
    nextGreater := make(map[int]int)
    stack := []int{}
    
    // Find the next greater element for each element in nums2
    for _, num := range nums2 {
        for len(stack) > 0 && stack[len(stack)-1] < num {
            top := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            nextGreater[top] = num
        }
        stack = append(stack, num)
    }
    
    // Find the next greater element for each element in nums1
    result := make([]int, len(nums1))
    for i, num := range nums1 {
        if val, found := nextGreater[num]; found {
            result[i] = val
        } else {
            result[i] = -1
        }
    }
    
    return result
}

  ```
  