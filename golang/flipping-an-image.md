
  # flipping-an-image

  ```golang
  func flipAndInvertImage(image [][]int) [][]int {
    n := len(image)
    
    // Iterate through each row of the image
    for i := 0; i < n; i++ {
        left := 0
        right := n - 1
        
        // Reverse the row
        for left < right {
            image[i][left], image[i][right] = image[i][right], image[i][left]
            left++
            right--
        }
        
        // Invert the row
        for j := 0; j < n; j++ {
            image[i][j] = 1 - image[i][j]
        }
    }
    
    return image
}

  ```
  