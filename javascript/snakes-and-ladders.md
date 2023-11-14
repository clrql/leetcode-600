
  # snakes-and-ladders

  ```javascript
  /**
 * @param {number[][]} board
 * @return {number}
 */
var snakesAndLadders = function(board) {
  const n = board.length;
  const target = n * n;
  const visited = new Array(n * n + 1).fill(false); // Mark cells as visited
  
  // Create a queue for BFS
  const queue = [];
  queue.push(1); // Start at square 1
  visited[1] = true; // Mark square 1 as visited
  
  let moves = 0;
  
  // Perform BFS
  while (queue.length > 0) {
    const size = queue.length;
    
    // Process all cells at the current level
    for (let i = 0; i < size; i++) {
      const curr = queue.shift();
      
      // Check if we have reached the target square
      if (curr === target) {
        return moves;
      }
      
      // Roll the die and explore all possible destinations
      for (let j = 1; j <= 6 && curr + j <= target; j++) {
        const next = curr + j;
        const [row, col] = getCoordinates(next, n);
        
        // Check if the next square has a snake or ladder
        const dest = board[row][col] === -1 ? next : board[row][col];
        
        // If the destination has not been visited, add it to the queue
        if (!visited[dest]) {
          visited[dest] = true;
          queue.push(dest);
        }
      }
    }
    
    moves++; // Increment the number of moves after processing all cells at the current level
  }
  
  return -1; // Target square cannot be reached
};

// Helper function to convert a square number to coordinates
function getCoordinates(square, n) {
  const row = Math.floor((square - 1) / n);
  const col = (square - 1) % n;
  
  // Adjust coordinates for Boustrophedon style
  if (row % 2 === 1) {
    return [n - 1 - row, n - 1 - col];
  }
  
  return [n - 1 - row, col];
}
  ```
  