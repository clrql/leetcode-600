
  # sort-by

  ```javascript
  /**
 * @param {Array} arr
 * @param {Function} fn
 * @return {Array}
 */
var sortBy = function(arr, fn) {
    if (arr.length <= 1) {
        return arr;
    }

    var mid = Math.floor(arr.length / 2);
    var left = arr.slice(0, mid);
    var right = arr.slice(mid);

    return merge(sortBy(left, fn), sortBy(right, fn), fn);
    };

function merge(left, right, fn) {
    var sorted = [];
    var leftIndex = 0;
    var rightIndex = 0;

    while (leftIndex < left.length && rightIndex < right.length) {
        if (fn(left[leftIndex]) <= fn(right[rightIndex])) {
        sorted.push(left[leftIndex]);
        leftIndex++;
        } else {
        sorted.push(right[rightIndex]);
        rightIndex++;
        }
    }

    while (leftIndex < left.length) {
        sorted.push(left[leftIndex]);
        leftIndex++;
    }

    while (rightIndex < right.length) {
        sorted.push(right[rightIndex]);
        rightIndex++;
    }

    return sorted;
};
  ```
  