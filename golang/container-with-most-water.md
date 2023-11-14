
  # container-with-most-water

  ```golang
  func maxArea(height []int) int {
    i, j := 0, len(height)-1
    maxArea := 0
    
    for i < j {
        area := min(height[i], height[j]) * (j-i)
        if area > maxArea {
            maxArea = area
        }
        
        if height[i] < height[j] {
            i++
        } else {
            j--
        }
    }
    
    return maxArea
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
  ```
  