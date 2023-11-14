
  # fair-candy-swap

  ```javascript
  /**
 * @param {number[]} aliceSizes
 * @param {number[]} bobSizes
 * @return {number[]}
 */
var fairCandySwap = function(aliceSizes, bobSizes) {
    const sumAlice = aliceSizes.reduce((acc, curr) => acc + curr, 0);
    const sumBob = bobSizes.reduce((acc, curr) => acc + curr, 0);
    const diff = (sumAlice - sumBob) / 2;

    const setBob = new Set(bobSizes);
    for (const candy of aliceSizes) {
        const target = candy - diff;
        if (setBob.has(target)) {
            return [candy, target];
        }
    }
};
  ```
  