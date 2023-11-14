
  # maximal-rectangle

  ```golang
  func maximalRectangle(matrix [][]byte) int {
    if len(matrix) == 0 {
        return 0
    }

    rows, cols := len(matrix), len(matrix[0])
    heights := make([]int, cols)
    maxArea := 0

    for row := 0; row < rows; row++ {
        for col := 0; col < cols; col++ {
            if matrix[row][col] == '1' {
                heights[col]++
            } else {
                heights[col] = 0
            }
        }
        maxArea = max(maxArea, largestRectangleArea(heights))
    }

    return maxArea
}

func largestRectangleArea(heights []int) int {
    stack := make([]int, 0)
    maxArea := 0
    n := len(heights)

    for i := 0; i <= n; {
        h := 0
        if i < n {
            h = heights[i]
        }

        if len(stack) == 0 || h >= heights[stack[len(stack)-1]] {
            stack = append(stack, i)
            i++
        } else {
            tp := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            width := i
            if len(stack) > 0 {
                width = i - stack[len(stack)-1] - 1
            }
            maxArea = max(maxArea, heights[tp]*width)
        }
    }

    return maxArea
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

  ```
  