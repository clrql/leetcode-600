
  # pascals-triangle

  ```javascript
  /**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    let pascalTriangle = [];
    for (let i = 0; i < numRows; i++) {
        if (i == 0) pascalTriangle.push([1]);
        if (i == 1) pascalTriangle.push([1, 1]);
        if (i >= 2) {
            let row = [1];
            for (let j = 0; j < pascalTriangle[i-1].length-1; j++) {
                let r = pascalTriangle[i-1][j] + pascalTriangle[i-1][j+1];
                row.push(r);
            }
            row.push(1);
            pascalTriangle.push(row);
        }
    }
    return pascalTriangle;
};
  ```
  