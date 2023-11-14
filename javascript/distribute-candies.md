
  # distribute-candies

  ```javascript
  /**
 * @param {number[]} candyType
 * @return {number}
 */
var distributeCandies = function(candyType) {
  const uniqueTypes = new Set(candyType);
  const maxEat = candyType.length / 2;
  
  return Math.min(uniqueTypes.size, maxEat);
};
  ```
  