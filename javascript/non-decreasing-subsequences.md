
  # non-decreasing-subsequences

  ```javascript
  /**
 * @param {number[]} nums
 * @return {number[][]}
 */
var findSubsequences = function(nums) {
    const result = [];
    function backtrack(current, start) {
        if (current.length >= 2) {
            result.push([...current]);
        }

        const used = new Set();
        for (let i = start; i < nums.length; i++) {
            if (used.has(nums[i]) || (current.length > 0 && nums[i] < current[current.length-1])) {
                continue;
            }
            used.add(nums[i]);
            current.push(nums[i]);
            backtrack(current, i + 1);
            current.pop();
        }
    }
    backtrack([], 0);
    return result;
};


  ```
  