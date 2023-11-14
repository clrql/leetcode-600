
  # restore-the-array-from-adjacent-pairs

  ```golang
  func restoreArray(adjacentPairs [][]int) []int {
    // Create a hashmap to store adjacent pairs
    adjacentMap := make(map[int][]int)

    // Fill the hashmap with adjacent pairs
    for _, pair := range adjacentPairs {
        u, v := pair[0], pair[1]
        adjacentMap[u] = append(adjacentMap[u], v)
        adjacentMap[v] = append(adjacentMap[v], u)
    }

    // Find the starting element (the one with only one adjacent pair)
    var start int
    for num, adjacents := range adjacentMap {
        if len(adjacents) == 1 {
            start = num
            break
        }
    }

    // Reconstruct the array using the adjacent pairs
    n := len(adjacentPairs) + 1
    result := make([]int, n)
    result[0] = start

    for i := 1; i < n; i++ {
        prev := result[i-1]
        next := adjacentMap[prev][0]
        result[i] = next

        // Remove the used adjacent pair to avoid revisiting it
        delete(adjacentMap, prev)
        adjacentMap[next] = removeValue(adjacentMap[next], prev)
    }

    return result
}

func removeValue(arr []int, val int) []int {
    for i, num := range arr {
        if num == val {
            return append(arr[:i], arr[i+1:]...)
        }
    }
    return arr
}

  ```
  