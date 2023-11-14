
  # pascals-triangle-ii

  ```javascript
  /**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    if (rowIndex < 0) {
        return [];
    }
    
    // Initialize the first row with a single element 1.
    let row = [1];
    
    for (let i = 1; i <= rowIndex; i++) {
        const newRow = [1]; // The first element of each row is always 1.
        for (let j = 1; j < row.length; j++) {
            newRow.push(row[j - 1] + row[j]);
        }
        newRow.push(1); // The last element of each row is always 1.
        
        row = newRow; // Update the current row.
    }
    
    return row;
};

  ```
  