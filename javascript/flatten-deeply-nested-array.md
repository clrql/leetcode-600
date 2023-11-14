
  # flatten-deeply-nested-array

  ```javascript
  /**
 * @param {any[]} arr
 * @param {number} depth
 * @return {any[]}
 */
var flat = function (arr, n) {
  function flattenHelper(arr, depth) {
    const flattened = [];
    for (const elem of arr) {
      if (Array.isArray(elem) && depth < n) {
        flattened.push(...flattenHelper(elem, depth + 1));
      } else {
        flattened.push(elem);
      }
    }
    return flattened;
  }
  
  return flattenHelper(arr, 0);
};

  ```
  