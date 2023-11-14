
  # island-perimeter

  ```javascript
  /**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
  var rows = grid.length;
  var cols = grid[0].length;
  var perimeter = 0;

  for (var i = 0; i < rows; i++) {
    for (var j = 0; j < cols; j++) {
      if (grid[i][j] === 1) {
        perimeter += 4;

        if (i > 0 && grid[i - 1][j] === 1) {
          perimeter -= 2;
        }

        if (j > 0 && grid[i][j - 1] === 1) {
          perimeter -= 2;
        }
      }
    }
  }

  return perimeter;
};
  ```
  