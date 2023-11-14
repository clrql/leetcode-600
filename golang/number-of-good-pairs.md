
  # number-of-good-pairs

  ```golang
  func numIdenticalPairs(nums []int) int {
    // Create a map to count the occurrences of each number
    numCounts := make(map[int]int)
    
    // Initialize the result variable to keep track of good pairs
    goodPairs := 0
    
    // Iterate through the nums array and update the counts in the map
    for _, num := range nums {
        numCounts[num]++
    }
    
    // Iterate through the map and calculate the number of good pairs
    for _, count := range numCounts {
        goodPairs += (count * (count - 1)) / 2
    }
    
    return goodPairs
}
  ```
  