
  # equal-row-and-column-pairs

  ```javascript
  /**
 * @param {number[][]} grid
 * @return {number}
 */
var equalPairs = function(grid) {
    let count = 0;
    const n = grid.length;

    // Keep track of the frequency of each row.
    const rowCounter = new Map();
    for (const row of grid) {
        const key = JSON.stringify(row);
        rowCounter.set(key, (rowCounter.get(key) || 0) + 1);
    }

    // Add up the frequency of each column in the map.
    for (let c = 0; c < n; c++) {
        const col = [];
        for (let i = 0; i < n; i++) {
            col.push(grid[i][c]);
        }
        const key = JSON.stringify(col);
        count += rowCounter.get(key) || 0;
    }

    return count;
};
  ```
  