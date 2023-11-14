
  # longest-harmonious-subsequence

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number}
 */
var findLHS = function(nums) {
  const freqMap = new Map();
  let maxLength = 0;
  
  // Count the frequencies of each number
  for (let num of nums) {
    freqMap.set(num, (freqMap.get(num) || 0) + 1);
  }
  
  // Iterate over the numbers and check for harmonious subsequence
  for (let [num, freq] of freqMap) {
    if (freqMap.has(num + 1)) {
      maxLength = Math.max(maxLength, freq + freqMap.get(num + 1));
    }
    if (freqMap.has(num - 1)) {
      maxLength = Math.max(maxLength, freq + freqMap.get(num - 1));
    }
  }
  
  return maxLength;
};

  ```
  