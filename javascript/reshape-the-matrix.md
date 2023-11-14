
  # reshape-the-matrix

  ```javascript
  /**
 * @param {number[][]} mat
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(mat, r, c) {
  const m = mat.length; // Number of rows in the original matrix
  const n = mat[0].length; // Number of columns in the original matrix

  // Check if the reshape operation is possible
  if (m * n !== r * c) {
    return mat; // Reshape is not possible, return the original matrix
  }

  // Flatten the original matrix into a 1D array
  const flattened = mat.flat();

  // Create the reshaped matrix
  const reshaped = [];
  let index = 0;

  // Fill the reshaped matrix with the elements from the flattened array
  for (let i = 0; i < r; i++) {
    const row = [];
    for (let j = 0; j < c; j++) {
      row.push(flattened[index]);
      index++;
    }
    reshaped.push(row);
  }

  return reshaped;
};
  ```
  