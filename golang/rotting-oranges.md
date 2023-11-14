
  # rotting-oranges

  ```golang
  func orangesRotting(grid [][]int) int {
    // Define the directions for 4-directional adjacency
    directions := [4][2]int{{-1, 0}, {0, 1}, {1, 0}, {0, -1}}

    // Initialize a queue to store the coordinates of rotten oranges
    queue := make([][2]int, 0)

    // Initialize variables to keep track of fresh oranges and the number of minutes elapsed
    freshOranges := 0
    minutesElapsed := 0

    // Step 1: Count the number of fresh oranges and enqueue the coordinates of rotten oranges
    rows := len(grid)
    cols := len(grid[0])
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if grid[i][j] == 1 {
                freshOranges++
            } else if grid[i][j] == 2 {
                queue = append(queue, [2]int{i, j})
            }
        }
    }

    // Step 2: Simulate the rotting process using BFS
    for len(queue) > 0 && freshOranges > 0 {
        // Keep track of the size of the current level/minute
        levelSize := len(queue)

        for i := 0; i < levelSize; i++ {
            orange := queue[0]
            queue = queue[1:]

            row := orange[0]
            col := orange[1]

            // Check the 4-directionally adjacent cells
            for _, dir := range directions {
                newRow := row + dir[0]
                newCol := col + dir[1]

                // Skip if the adjacent cell is out of bounds or contains a rotten or empty orange
                if newRow < 0 || newRow >= rows || newCol < 0 || newCol >= cols || grid[newRow][newCol] != 1 {
                    continue
                }

                // Mark the adjacent fresh orange as rotten and enqueue its coordinates
                grid[newRow][newCol] = 2
                queue = append(queue, [2]int{newRow, newCol})
                freshOranges--
            }
        }

        // Increment the number of minutes elapsed
        if len(queue) > 0 {
            minutesElapsed++
        }
    }

    // Step 3: Return the result based on the remaining fresh oranges
    if freshOranges == 0 {
        return minutesElapsed
    }

    return -1
}

  ```
  