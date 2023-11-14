
  # kids-with-the-greatest-number-of-candies

  ```javascript
  /**
 * @param {number[]} candies
 * @param {number} extraCandies
 * @return {boolean[]}
 */
var kidsWithCandies = function(candies, extraCandies) {
    const greatest = [];
    candies.forEach((kidcandies, kidcandiesindex) => {
        const sum = kidcandies + extraCandies;
        greatest.push(true);
        candies.forEach((kidcandies2, kidcandiesindex2) => {
            if (kidcandiesindex2 != kidcandiesindex) {
                if (kidcandies2 > sum) {
                    greatest[kidcandiesindex] = false;
                }
            }
        });
    });
    return greatest;
};
  ```
  