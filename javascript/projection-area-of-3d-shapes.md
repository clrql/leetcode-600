
  # projection-area-of-3d-shapes

  ```javascript
  /**
 * @param {number[][]} grid
 * @return {number}
 */
var projectionArea = function(grid) {
    let n = grid.length;
    let xyProjection = 0;
    let xzProjection = 0;
    let yzProjection = 0;

    for (let i = 0; i < n; i++) {
        let maxRow = 0;
        let maxCol = 0;

        for (let j = 0; j < n; j++) {
            if (grid[i][j] > 0) {
                xyProjection++;
            }
            maxRow = Math.max(maxRow, grid[i][j]);
            maxCol = Math.max(maxCol, grid[j][i]);
        }

        xzProjection += maxRow;
        yzProjection += maxCol;
    }

    const totalArea = xyProjection + xzProjection + yzProjection;

    return totalArea;
};
  ```
  