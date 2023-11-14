
  # minimum-index-sum-of-two-lists

  ```javascript
  /**
 * @param {string[]} list1
 * @param {string[]} list2
 * @return {string[]}
 */
var findRestaurant = function(list1, list2) {
  const map = new Map();
  let minIndexSum = Infinity;
  const result = [];
  
  // Store the index of each string in list1
  for (let i = 0; i < list1.length; i++) {
    map.set(list1[i], i);
  }
  
  // Check for common strings and update the minimum index sum
  for (let j = 0; j < list2.length; j++) {
    if (map.has(list2[j])) {
      const indexSum = j + map.get(list2[j]);
      if (indexSum < minIndexSum) {
        minIndexSum = indexSum;
        result.length = 0; // Clear the previous result
        result.push(list2[j]);
      } else if (indexSum === minIndexSum) {
        result.push(list2[j]);
      }
    }
  }
  
  return result;
};

  ```
  