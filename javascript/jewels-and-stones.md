
  # jewels-and-stones

  ```javascript
  /**
 * @param {string} jewels
 * @param {string} stones
 * @return {number}
 */
var numJewelsInStones = function(jewels, stones) {
    let count = 0;
    while (jewels.length) {
        let curr = jewels[0];
        let previus = stones;
        jewels = jewels.replaceAll(curr, "");
        stones = stones.replaceAll(curr, "");
        count += previus.length - stones.length;
    }
    return count;
};
  ```
  