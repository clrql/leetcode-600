
  # find-k-closest-elements

  ```javascript
  /**
 * @param {number[]} arr
 * @param {number} k
 * @param {number} x
 * @return {number[]}
 */
var findClosestElements = function(arr, k, x) {
    arr.sort((a, b) => {
        const 
        a1 = Math.abs(a-x),
        b1 = Math.abs(b-x);
        return a1 == b1 ? a-b : a1-b1;
    });
    return arr.splice(0,k).sort((a,b) => a-b);
};
  ```
  