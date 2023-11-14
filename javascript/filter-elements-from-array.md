
  # filter-elements-from-array

  ```javascript
  /**
 * @param {number[]} arr
 * @param {Function} fn
 * @return {number[]}
 */
var filter = function(arr, fn) {
    const filtered = [];
    for (let i = 0; i < arr.length; i++) {
        const result = fn(arr[i], i);
        if (result) filtered.push(arr[i]);
    }
    return filtered;
};
  ```
  