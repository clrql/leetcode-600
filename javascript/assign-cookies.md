
  # assign-cookies

  ```javascript
  /**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function(g, s) {
    g.sort((a, b) => a - b); // Sort greed factors in ascending order
  s.sort((a, b) => a - b); // Sort cookie sizes in ascending order

  let contentChildren = 0;
  let cookieIndex = 0;

  for (let i = 0; i < g.length; i++) {
    while (cookieIndex < s.length && s[cookieIndex] < g[i]) {
      cookieIndex++;
    }

    if (cookieIndex < s.length) {
      contentChildren++;
      cookieIndex++;
    } else {
      break; // No more cookies available
    }
  }

  return contentChildren;
};
  ```
  