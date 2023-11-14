
  # chunk-array

  ```javascript
  /**
 * @param {Array} arr
 * @param {number} size
 * @return {Array[]}
 */
var chunk = function(arr, size) {
    let chunks = [];
    while (arr.length) {
        chunks.push([]);
        for (let i = 0; i<size; i++) {
            if (!arr.length) break;
            chunks[chunks.length-1].push(arr.shift());
        };
    };
    return chunks;
};
  ```
  