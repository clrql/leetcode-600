
  # binary-gap

  ```javascript
  /**
 * @param {number} n
 * @return {number}
 */
var binaryGap = function(n) {
    const binaryString = n.toString(2);
    let maxGap = 0;
    let currentGap = 0;
    let foundOne = false;
    for (let i = 0; i < binaryString.length; i++) {
        if (binaryString[i] === "1") {
            if (foundOne) {
                maxGap = Math.max(maxGap, currentGap)
            }
            currentGap = 1;
            foundOne = true;
        } else {
            if (foundOne) {
                currentGap++;
            }
        }
    }
    return maxGap;
};
  ```
  