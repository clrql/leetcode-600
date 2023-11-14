
  # search-a-2d-matrix

  ```javascript
  /**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function(matrix, target) {
  if (matrix.length === 0 || matrix[0].length === 0) {
    return false;
  }
  
  const rows = matrix.length;
  const columns = matrix[0].length;
  let left = 0;
  let right = rows * columns - 1;
  
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    const midValue = matrix[Math.floor(mid / columns)][mid % columns];
    
    if (midValue === target) {
      return true;
    } else if (midValue < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  
  return false;
};
  ```
  