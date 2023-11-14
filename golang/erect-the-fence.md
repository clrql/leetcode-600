
  # erect-the-fence

  ```golang
  func outerTrees(trees [][]int) [][]int {
    n := len(trees)
    if n <= 1 {
        return trees
    }
    
    // Sort the trees based on their x-coordinates (and y-coordinates in case of ties).
    sort.Slice(trees, func(i, j int) bool {
        if trees[i][0] == trees[j][0] {
            return trees[i][1] < trees[j][1]
        }
        return trees[i][0] < trees[j][0]
    })
    
    // Initialize two sets to keep track of the upper and lower hulls.
    upperHull, lowerHull := make([][]int, 0), make([][]int, 0)
    
    // Build the upper hull.
    for i := 0; i < n; i++ {
        for len(upperHull) >= 2 && cross(upperHull[len(upperHull)-2], upperHull[len(upperHull)-1], trees[i]) < 0 {
            upperHull = upperHull[:len(upperHull)-1]
        }
        upperHull = append(upperHull, trees[i])
    }
    
    // Build the lower hull.
    for i := n - 1; i >= 0; i-- {
        for len(lowerHull) >= 2 && cross(lowerHull[len(lowerHull)-2], lowerHull[len(lowerHull)-1], trees[i]) < 0 {
            lowerHull = lowerHull[:len(lowerHull)-1]
        }
        lowerHull = append(lowerHull, trees[i])
    }
    
    // Combine the upper and lower hulls to get the final result.
    result := append(upperHull[:len(upperHull)-1], lowerHull[:len(lowerHull)-1]...)
    
    // Remove duplicates from the result.
    uniqueResult := make([][]int, 0)
    uniqueSet := make(map[[2]int]bool)
    for _, point := range result {
        if !uniqueSet[[2]int{point[0], point[1]}] {
            uniqueSet[[2]int{point[0], point[1]}] = true
            uniqueResult = append(uniqueResult, point)
        }
    }
    
    return uniqueResult
}

func cross(p1, p2, p3 []int) int {
    return (p2[0]-p1[0])*(p3[1]-p1[1]) - (p2[1]-p1[1])*(p3[0]-p1[0])
}

  ```
  