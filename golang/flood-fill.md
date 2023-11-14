
  # flood-fill

  ```golang
  func floodFill(image [][]int, sr int, sc int, newColor int) [][]int {
    if image[sr][sc] == newColor {
        return image
    }
    fill(image, sr, sc, image[sr][sc], newColor)
    return image
}

func fill(image [][]int, sr int, sc int, originalColor int, newColor int) {
    if sr < 0 || sr >= len(image) || sc < 0 || sc >= len(image[0]) || image[sr][sc] != originalColor {
        return
    }
    image[sr][sc] = newColor
    fill(image, sr+1, sc, originalColor, newColor) // Down
    fill(image, sr-1, sc, originalColor, newColor) // Up
    fill(image, sr, sc+1, originalColor, newColor) // Right
    fill(image, sr, sc-1, originalColor, newColor) // Left
}

  ```
  