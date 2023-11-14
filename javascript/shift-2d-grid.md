
  # shift-2d-grid

  ```javascript
  /**
 * @param {number[][]} grid
 * @param {number} k
 * @return {number[][]}
 */
var shiftGrid = function(grid, k) {
    let m = grid[0].length;
    grid = grid.join().split(",");
    for (let i = 0; i < k; i++) {
        grid.unshift(grid.pop());
    }
    for (let i = 0; i < grid.length; i += m) {
        grid[i] = grid.slice(i, i+m);
    }
    return grid.filter(e => Array.isArray(e));
};
  ```
  